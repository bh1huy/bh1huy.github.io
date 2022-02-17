#### [非智能电视看高清免费IPTV电视直播](https://www.toutiao.com/a7026696296916419084/?log_from=face56a5183cb_1636799133662)

尽管现在可以安装APP的安卓智能电视越来越普及了，但是我相信在此之前有很多人为了某些需求（比如开机快、开机免广告、系统简洁、画质好等）不得不选择LG的webos和三星Tizen等半智能电视。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/c3678c60995c45a4985a7a841e829c7c?from=pc)

LG websos电视

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/b292f3d09eaa47379161df6bce7c156f?from=pc)

三星tizen电视

这些电视不能像安卓智能电视那样可以安装电视猫、电视家之类的电视直播软件，我们想看个电视直播不得不插上有线电视或宽带运营商的IPTV机顶盒。我之前租房时为了把电视接入开源的homeassistant智能家居平台，就买了一个43寸的LG webos的电视。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/2bfbb10b6e6f496b943d163ffcfa63a1?from=pc)

自从买了华为智慧屏，它就退居卧室了。偶尔睡前看个电视，且为了保持电视周边简洁好看，我不想再放个电视盒子，于是就有这篇不用机顶盒不用装软件，非智能电视只要支持dlna功能的电视就可以看高清免费IPTV电视直播的方法。

这个方法的原理就是利用华硕路由（可以刷机padavan或openwrt的路由器也可以）自带的IPTV功能加自行安装XUPnPd软件把IPTV电视直播转换成视频文件。最终实现**电视不安装软件，免费、免广告干扰，看高清、稳定、不占上网带宽deIPTV电视直播**的目的。整个的原理图如下图所示。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/cc3ed13440324f1fab7a7a8d593aa88a?from=pc)

##### 一、华硕路由IPTV设置

关于如何把IPTV接入路由器（家庭局域网）每个地区可能不太一样，大体上分不需要鉴权的DHCP、需要账号鉴权的PPPoE（类似宽带账号）、需要鉴权的IPoE（DHCP+）。这三种情况理论上都可以把IPTV接入路由局域网。我用的联通宽带的IPTV很幸运是最简单的DHCP，不需要鉴权。下面我就以自己的IPTV接入华硕路由器原厂不刷机固件为例给大家介绍。

**1. 光猫设置**

作为爱折腾的数码玩家，我已经自己用华为四口千兆光猫换掉了原来的只有一个千兆口的中兴光猫，我也拿到了光猫的超级管理员账号密码，也把光猫中的上网模式由路由模式改为桥接模式（即路由器替代光猫进行宽带拨号），而且我去修改了光猫的端口绑定，让每个口都可以上网和看IPTV。也在此预告后续给大家分享如何更换光猫、如何光猫改桥接、如何上网和IPTV单线复用、如何抓包IPTV直播源。下图是我的光猫设置，IPTV和Internet都绑定了所有端口。如果你家的光猫每个lan口都可以上网及看IPTV，大概率就是两者没绑定端口，或者绑定了所有端口。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/815502d42a4142a28b87d65c07daea09?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/3f7d3027cd7c4f8baedda6fd22cea939?from=pc)

**2. 路由器iptv和udpxy设置**

华硕路由器设置如下：点击“内部网络（lan）”然后切换到“IPTV”按下图设置即可。网上绝大部分的IPTV和上网单线复用的都是采用的vlan绑定，都要在这里填入valn ID，我这种光猫没进行vlan绑定的，IPTV这里就不需要填入vlan ID。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/e0f36983e8144848b5bf75684aa7e745?from=pc)

路由器外网部分正常填入宽带账号密码即可上网了。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/d8c40284620e43e88dd1155ac0d50306?from=pc)

此时查看外网连接状态，你会发现你的路由器获得了两个IP地址，一个是上网的外网IP，一个是光猫分配的192.168开头的IPTV网络的IP。这样你就把上网和IPTV同时接入你的路由器构建的局域网了，同时也配置好了udpxy，现在你就可以用你原来的IPTV机顶盒插入路由器lan4口看IPTV了，但是如果你没开IPTV，你看不了，但是你可以从网上搜到的你本地区的IPTV直播源用kodi等软件免费看IPTV了。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/7187ff6a326e4723b0d6ec21a1226572?from=pc)

假如你在网上搜到的本地区（切记是本地区哈，IPTV是分区域独立部署的，跨区的组播直播源是用不了的）直播源其中某台的地址为rtp:239.3.1.78:4120,你现在替换成http://你的路由器管理
IP:8686/rtp/239.3.1.78:4120就可以点播IPTV了。你可以用notepad++软件进行批量替换，生成新的http点播直播源。到此你已经可以用kodi或VLC等播放软件直接打开http://你的路由器管理IP:8686/rtp/239.3.1.78:4120看电视直播了。当然你也可以自己抓直播源

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/ca5d788bb6cc46eab19a4d113af5d0c9?from=pc)

但是如果你的电视不支持安装这些软件，我们就需要路由器安装XUPNPD软件把http的视频流转换成我们常见的视频文件，用电视自带的媒体播放器点播IPTV。

##### 二、华硕安装XUPNP软件

华硕官方固件默认没有XUPNP（老毛子基于华硕固件改版的padavan集成该软件），但是我们可以自行安装。

**1. 插入u盘到路由器**

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/49b7295f02464cb6bfa660aadc9cff9a?from=pc)

格式化U盘，格式一定要选NTFS，不要用默认的FAT，否则安装软件时会报错。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/49eb1062b7b94a12946c24c11284a7d9?from=pc)

**2. 启用下载大师**

点击“USB相关应用”。然后选择“下载大师”进行安装，安装下载大师会自动部署optware环境，安装完成你可以禁用或卸载下载大师。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/da8b315a7ed94ef1a0fe037d320a0871?from=pc)

**3. 安装XUPNP**

① 按下图操作打开路由器的ssh

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/9c2e78968d2b47049243eab142fe9644?from=pc)

② 打开电脑上的putty软件（没安装的请自行搜索安装），按下图设置打开对话框（此时电脑必须在路由器的局域网网络中）

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/6794ce4a5408411f9cccdc61400755de?from=pc)

③ 输入你路由器管理界面的登录账号和密码完成与路由器的连接。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/3bc6b87b8c944702b52001c1f5573dae?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/8b66056e07bc41fba2084366b749941f?from=pc)

④ 升级软件包，输入ipkg update回车，再输入ipkg upgrade完成软件包更新升级

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/1e9893eb31ac496a84c48468ab9bed24?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/3d77bbf71a434e3782460cd504a76066?from=pc)

⑤ 安装XUPNPD软件，输入命令“ipkg install xupnpd"回车进行安装即可。

**4. 设置XUPNP自启动**

① 打开winscp软件（没有请自行搜索安装），输入你的路由器IP地址和账号密码等信息，点击“登录”，完成连接路由器

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/c1a2a92817b44688a3c944673856a437?from=pc)

② 按下图切换到根目录

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/086bc23bcd904544ab1015f399980229?from=pc)

③ 按下图路径找到xupnpd.control文件

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/6fb9b8aa62944a19936537b90de016e3?from=pc)

④ 按下图编辑xupnpd.control文件，在文件后添加“Enabled：yes”，然后保存。重启路由后xupnpd也会自动启动，再也不用手动启动了。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/9123b5a6adff432294600f765cf4ffb5?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/82227ab05e7e42a88924b53864bf2f62?from=pc)

⑤ 上传你的路由器IP版的直播源地址文件

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/8d8ff4d109d74819b7e2e367323c6a6f?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/64c43e24b5de4c39b25b66c72ef95afe?from=pc)

##### 三、畅享IPTV电视直播

现在我们就可以畅享高清稳定的免费IPTV电视直播了

**1. 电脑自带媒体播放器**

Windows系统自带的媒体播放器Windows media palyer在媒体库中可以自动发现同一局域网的UPNP-IPTV资源

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/49a88f87d4ed4c61993d342cd50efaa5?from=pc)

点击即可播放对应的电视频道直播

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/b0cad25925144e72b14806bbbd357efd?from=pc)

**2. LG webos等支持DLAN的设备**

以LG webos为例，打开电视自带的“照片和视频”应用，它会自动发现位于同一局域网内的DLNA服务器。点击自动发现的"UPnP-IPTV"文件夹。

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/02a3c540c1cf4068b64cacbbac9e6b0d?from=pc)

点击你想看的电视频道即可播放，享受高清、稳定的电视直播了

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/dff7aa92717049338e00fc535e0d9dfc?from=pc)

![不用机顶盒不用装软件，非智能电视也能看高清免费IPTV电视直播](https://p9.toutiaoimg.com/origin/pgc-image/e043de2993734ebfaa8fcf351c9a6c74?from=pc)

