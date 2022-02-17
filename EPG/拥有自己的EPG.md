#### [**拥有自己的EPG**](https://www.right.com.cn/FORUM/thread-4017075-1-1.html)

本来打算过几天再写，但一想明天就过节了，可以方便大家折腾，所以改在今天发表，先祝大家节日快乐。下面转入正题：首先你必须有可操作的路由器（当然如果你是土豪花钱租服务器，当我没说）我用的是`openwrt`，官方的自带curl命令，第三方多不带，你要自己安装，`wget`都支持，但用做爬取不如curl好用。我的压缩包总共3个文件：`tvsou.txt` |`tvsou.sh` | `tvsouchannel.txt`。文件运行只用前两个，你需要做的就是从`tvsouchannel.txt`中找出你喜欢的频道，把它复制粘贴到`tvsou.txt`里面，不要把后面的网址也粘贴进去，那是台标，不能有空行。前面的数字是对应频道的ID，这个不能改，后面的频道名称可以改，二者之间必须有空格或者TAB，至于没有的地方台，请去网站自己取。有些节目单只有你的运营商有，你必须提取转换后才能用，由于不通用，我没有把我自己用的发上来。然后把这两个文件想办法弄到路由器里，放哪里无所谓，我是在根目录。但是请不要放在`/tmp`等目录下，那是内存，机器重启就没有了。然后命令行`sh /tvsou.sh`(根据你放的目录，这里是根目录）就运行了。然后到计划任务那里添加如下： `* 6 * * * sh /tvsou.sh`(根据你放的目录，这里是根目录） 意思是每天早上6点运行，时间你可以改，然后到浏览器打开`192.168.x.1/epg/tvsou.xml`，测试有没有完美运行，若行就添加到盒子里头就行了。如果你是组播，那你应该做内网穿透或者`DDNS`来再来访问      

- ![img](https://www.right.com.cn/FORUM/static/image/filetype/rar.gif)
  [tvsou.rar](https://www.right.com.cn/FORUM/forum.php?mod=attachment&aid=MzgwNDUzfDQ2Y2RkNzdifDE2MzgyNTU1NjJ8MHw0MDE3MDc1)

- ![img](https://www.right.com.cn/FORUM/static/image/filetype/rar.gif)
  [tvmao.rar](https://www.right.com.cn/FORUM/forum.php?mod=attachment&aid=MzkzOTgyfDVkZDBjN2NkfDE2MzgyNTU1NjJ8MHw0MDE3MDc1)

##### tvsou.sh

```bash
#!/bin/bash
#
#tvsou.sh
#

#到内存中运行
cp /tvsou.txt /tmp/
cd  /tmp
#计算频道数以便抓取每行每列的数据
n=`grep -c '^.*$' tvsou.txt`
#写入文件头
echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>" >/www/epg/tvsou.xml
echo "<tv >" >>/www/epg/tvsou.xml
for i in $(seq 1 $n)
do
chid=`sed -n ${i}p tvsou.txt | awk '{print $1}'` 
chname=`sed -n ${i}p tvsou.txt | awk '{print $2}'`
#当前年月日
d=`date +%Y%m%d`
curl https://www.tvsou.com/epg/${chid}/ \
| sed -n '/<tr><td><a href/p' \
| sed  -e '2,$d' | sed 's/<\/tr>/<\/tr>\n/g'  \
| sed -n '/<tr><td>/p' \
| sed 's/.*target=..blank.>\([0-9][0-9]\):\([0-9][0-9]\).*target=..blank.>\(.*\)<\/a>.*/\1\2\t\3/g'  \
| awk '{if ($0!=line) print;line=$0}' \
| sed  's/\([0-9]\{4\}\)\t/'$d'\100\taaaa\t/g' \
| sed ':a;N;s/\(aaaa\)\t\(.*\)\n\([0-9]\{14\}\)/\3\t\2\n\3/;ta;'\
| sed 's/\r//g' | sed 's/<\(.*\)>/《\1》/g'   >shuju.txt
#判断有没有抓到数据
if [ -s  shuju.txt ] ; then
echo "<channel id=\"${chname}\">" >>/www/epg/tvsou.xml
echo "<display-name lang=\"zh\">${chname}</display-name>" >>/www/epg/tvsou.xml
echo "</channel>" >>/www/epg/tvsou.xml; 
fi
while  read start stop jm
do
#判断是不是最后一行
if [[ $stop == aaaa ]]
then
stop="$d"235900
else stop=$stop
fi
#写入节目单
echo "<programme start=\"$start +0800\" stop=\"$stop +0800\" channel=\"${chname}\">" >>tvsou1.xml
echo "<title lang=\"zh\">$jm</title>" >>tvsou1.xml
echo "</programme>" >>tvsou1.xml
done <shuju.txt
done
echo "</tv>" >>tvsou1.xml
cat tvsou1.xml >>/www/epg/tvsou.xml
rm -f tvsou1.xml
exit
```

##### tvsou.txt

```text
b3666b9d CCTV-1综合
c5717c2d CCTV-2财经
53eda06f CCTV-3综艺
0ccc41bf CCTV-4国际
6b26bee1 CCTV-5体育
ddb707c0 CCTV-6电影
f2d13f2a CCTV-7国防军事
13e8f054 CCTV-8电视剧
8f932b7b CCTV-9纪录
7651a0a2 CCTV-10科教
0a2de840 CCTV-11戏曲
1e983148 CCTV-12法制
f5b1a323 CCTV-13新闻
6fff4f43 CCTV-14少儿
3201ff16 CCTV-15音乐
d3d48ldf CCTV-17
27360dbd 都市剧场
03dbf833 欢笑剧场
95c486cd SITV经典剧场
7c3ff471 纪实人文频道
4aab747c 山东齐鲁频道
7e7932bf 山东体育频道
35ff84e3 山东农科频道
d71d98ea 山东公共频道
db502561 淄博新闻综合
9e7598e6 淄博公共频道
83ef961b 淄博生活法治频道
b025804a 淄博都市频道
88508ef5 淄博科教频道
3db84aa3 华数欧美影院
a867cdd6 华数探索纪录
7efbe451 华数亚洲影院
bdceca9d 华数精品剧场
51e1655d 凤凰卫视
5d082b63 凤凰卫视资讯台
0e190daa 弈坛春秋
eda68f32 新娱乐
```

##### tvmao.sh

```bash
#!/bin/bash
#
# tvmao.sh
#

cp /tvmao.txt /tmp/
cd  /tmp
#计算频道数以便抓取每行每列的数据
n=`grep -c '[^^$]' tvmao.txt`
d=`date "+%Y%m%d"`
w=`date "+%w"`
if [[ $w == 0 ]]
then w=7
else w=$w
fi
keystr="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/="
#写入文件头
echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>" >/www/epg/tvmao.xml
echo "<tv >" >>/www/epg/tvmao.xml
for i in $(seq 1 $n)
do
chid=` awk 'NR=="'"$i"'"{print $1}' tvmao.txt` 
chname=` awk 'NR=="'"$i"'"{print $2}' tvmao.txt` 
curl  https://www.tvmao.com/${chid}-w${w}.html  >shangwu.txt
q=` cat shangwu.txt|grep  "form method"|cut -f10 -d'"'`
a=` cat shangwu.txt|grep  "form method"|cut -f12 -d'"'`
id=`cat shangwu.txt|grep  "猫一把"|cut -f10 -d'"'`
s1=$(($w*$w))
s1=${keystr:$s1:1}
s2=`echo -n "$id|$a" | base64 -w 0`
s3=`echo -n "|$q" | base64 -w 0`
curl https://www.tvmao.com/api/pg?p=${s1}${s2}${s3}    >>shangwu.txt
cat shangwu.txt | grep  "[0-9]\{2\}:[0-9]\{2\}"|  sed 's/\\n/\n/g' \
|sed  's#\\\/#\/#g' \
|sed 's/.*\([0-9]\{2\}:[0-9]\{2\}\).*\(<span.*<\/span>\).*/\1\t\2/' \
| sed "s/<[^>]*>//g" \
| sed -n 's/.*\([0-9]\{2\}\):\([0-9]\{2\}\)\(.*\)/'$d'\1\200\taaaa\t\3/p' \
| sed ':a;N;s/\(aaaa\)\t\(.*\)\n\([0-9]\{14\}\)/\3\t\2\n\3/;ta;'\
| sed 's/\r//g' | sed 's/<\(.*\)>/《\1》/g'    >shuju.txt
#判断有没有抓到数据
if [ -s  shuju.txt ] ; then
echo "<channel id=\"${chname}\">" >>/www/epg/tvmao.xml
echo "<display-name lang=\"zh\">${chname}</display-name>" >>/www/epg/tvmao.xml
echo "</channel>" >>/www/epg/tvmao.xml; 
fi
while  read start stop jm
do
#判断是不是最后一行
if [[ $stop == aaaa ]]
then
stop="$d"235900
else stop=$stop
fi
#写入节目单
echo "<programme start=\"$start +0800\" stop=\"$stop +0800\" channel=\"${chname}\">" >>tvmao1.xml
echo "<title lang=\"zh\">$jm</title>" >>tvmao1.xml
echo "</programme>" >>tvmao1.xml
done <shuju.txt
done
echo "</tv>" >>tvmao1.xml
cat tvmao1.xml >>/www/epg/tvmao.xml
rm -f tvmao1.xml
exit
```

##### tvmao.txt

```text
program/CCTV-CCTV1	CCTV-1
program/CCTV-CCTV2	CCTV-2
program/CCTV-CCTV3	CCTV-3
program/CCTV-CCTV4	CCTV-4
program/CCTV-CCTV5	CCTV-5
program/CCTV-CCTV6	CCTV-6
program/CCTV-CCTV7	CCTV-7
program/CCTV-CCTV8	CCTV-8
program/CCTV-CCTV9	CCTV-9
program/CCTV-CCTV10	CCTV-10
program/CCTV-CCTV11	CCTV-11
program/CCTV-CCTV12	CCTV-12
program/CCTV-CCTV13	CCTV-13
program/CCTV-CCTV15	CCTV-14
program/CCTV-CCTV16	CCTV-15
program/CCTV-CCTV17NY	CCTV-17
program/CCTV-CCTV5-PLUS	CCTV-5+
program_satellite/AHTV1	安徽卫视
program_satellite/BTV1	北京卫视
program_satellite/BTV10	卡酷少儿
program_satellite/CCQTV1	重庆卫视
program_satellite/FJTV2	东南卫视
program_satellite/XMTV5	厦门卫视
program_satellite/GSTV1	甘肃卫视
program_satellite/GDTV1	广东卫视
program_satellite/SZTV1	深圳卫视
program_satellite/NANFANG2	南方卫视
program_satellite/GUANXI1	广西卫视
program_satellite/GUIZOUTV1	贵州卫视
program_satellite/TCTC1	海南卫视
program_satellite/HEBEI1	河北卫视
program_satellite/HLJTV1	黑龙江卫视
program_satellite/HNTV1	河南卫视
program_satellite/HUBEI1	湖北卫视
program_satellite/HUNANTV1	湖南卫视
program_satellite/HUNANTV2	金鹰卡通
program_satellite/JSTV1	江苏卫视
program_satellite/JXTV1	江西卫视
program_satellite/JILIN1	吉林卫视
program_satellite/LNTV1	辽宁卫视
program_satellite/NMGTV1	内蒙古卫视
program_satellite/NXTV2	宁夏卫视
program_satellite/SXTV1	山西卫视
program_satellite/SDTV1	山东卫视
program_satellite/DONGFANG1	东方卫视
program_satellite/TOONMAX1	哈哈炫动
program_satellite/SHXITV1	陕西卫视
program_satellite/SCTV1	四川卫视
program_satellite/TJTV1	天津卫视
program_satellite/XJTV1	新疆卫视
program_satellite/YNTV1	云南卫视
program_satellite/ZJTV1	浙江卫视
program_satellite/QHTV1	青海卫视
program_satellite/XIZANGTV2	西藏卫视
program_satellite/YANBIAN1	延边卫视
program_satellite/BINGTUAN	兵团卫视
program_satellite/HXTV	海峡卫视
program_satellite/HHWS	黄河卫视
program_satellite/SANSHATV	三沙卫视
program/CCTVPAYFEE-SHUOWENJIEZI	国学
program/CCTVPAYFEE-XINKEDONGMAN	新科动漫
program/BAMC-BAMC1	车迷频道
program/BAMC-BAMC3	优优宝贝
program/BAMC-BAMC4	四海钓鱼
program/BAMC-BAMC7	新娱乐
program/BAMC-BAMC10	弈坛春秋
program/BAMC-ZHTCTV	中华特产
program/HSCM-QSJL	求索纪录
program/HSCM-QSSH	求索生活
program/HSCM-QSDW	求索动物
program/HSCM-QSKX	求索科学
program_digital/IPTVXSXP	相声小品
program_digital/IPTVFZ	法治
program/SITV-SITV3	法治天地
program/SITV-SITV6	金色频道
program/SITV-SITV9	极速汽车
program/SDTV-SDTV2	山东齐鲁
program/SDTV-SDTV3	山东体育
program/SDTV-SDTV4	山东农科
program/SDTV-SDTV5	山东公共
program/SDTV-SDTV6	山东少儿
program/SDTV-SDTV7	山东影视
program/SDTV-SDTV8	山东综艺
program/SDETV-SDETV1	山东教育
program/SDCATV-YZDY	亚洲电影
program/SDCATV-OMDY	欧美电影
program/SDCATV-YCH	演唱会
program/ZBRT-ZBRT3	淄博生活
program/ZBRT-ZBRT4	淄博都市
program/ZBRT-ZBRT5	淄博科教
program/NFCM-IPTVRBJC	热播剧场
program/NFCM-IPTVMLSS	魅力时尚
program/NFCM-IPTVSEDH	少儿动画
program/NFCM-IPTVJDDY	经典电影
program/SITV-SITV-MOVIE	都市剧场
program/SITV-SITV-DOCUMENTARY	全纪实
program/SITV-SITV-MOVIES	欢笑剧场
program/SITV-SITV-FASHION	生活时尚
program/SITV-SITV-CHILDREN	动漫秀场
program/SHHAI-SHHAI6	纪实人文
```

