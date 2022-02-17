#### [给Kodi直播电视添加电子节目单 节目播出表显示播放节目与时间](http://www.kodiplayer.cn/course/2925.html)

我们已经通过kodi可以看电视直播了（教程地址：http://www.kodiplayer.cn/course/2871.html），如果能够加上实时节目表，知晓未来播放什么节目那就更完美了。

EPG就是Electronic Program Guide的英文缩写，意思是电子节目指南。

节目表网站推荐：

```http
http://tv.cctv.com/epg/
https://www.tvmao.com/program   # 国内及港澳主要使用<电视猫>节目内容
https://www.tvsou.com/epg/
https://www.tbc.net.tw/Epg      # 台湾主要使用<TBC>节目内容
```

通过抓取CCTV、电视猫等节目表网站，就能制作xml格式的节目单，如果你爱折腾想自己做节目单，教程地址： https://blog.csdn.net/wlj1012/article/details/80742155。

我们采用网友分享的节目单设置KODI上的电视指南。

1\. 打开插件-我的插件 - `PVR IPTV Simple Client`

![img](http://www.kodiplayer.cn/UploadFiles/2019-04/2019041715051925175.jpg)

2\. 点击左下角“设置”，“常规”里面已经有我们以前添加的`m3u8`节目源，不需要再改动。

![img](http://www.kodiplayer.cn/UploadFiles/2019-04/2019041715105122341.jpg)

3\. 打开第二个选项“电子节目单设置”，`XMLTV URL`里填入<http://epg.51zmt.top:8000/e.xml>确定保存。（此节目单来自恩山大神supzhang，节目单包含最近两天的节目，频道有：央视，各省卫视、四川省台及成都台、山东频道、卡酷、金鹰、凤凰、港澳地区部分频道,台湾大部分频道等。）

![img](http://www.kodiplayer.cn/UploadFiles/2019-06/2019062710093535861.jpg)

4\. 重启kodi，打开电视，可以看到电视指南了。

“电视”--“指南”界面

![img](http://www.kodiplayer.cn/UploadFiles/2019-06/2019062710161296860.jpg)

电视直播界面

![img](http://www.kodiplayer.cn/UploadFiles/2019-06/2019062710134120755.jpg)

有的朋友添加完毕后会不能显示部分频道的节目单，解决方法如下：

你的`m3u8`文件频道命名需要和节目单里的频道名称一致，否则会匹配不到频道导致看不到节目单。

可以用下载工具下载下来<http://epg.51zmt.top:8000/e.xml>这个文件，用记事本打开，以CCTV1为例：

```m3u
<channel id="CCTV-CCTV1">
<display-name>CCTV1</display-name>
</channel>
```

用记事本打开m3u8文件：

```m3u
#EXTINF:-1 ,CCTV1
http://150.138.8.143/00/SNM/CHANNEL00000311/index.m3u8
```

以节目单display-name里的命名为准，修改你的`m3u8`里“`#EXTINF:-1 ,`”后面的名称，以此类推修改其他频道名称。