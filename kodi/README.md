#### 一、时间同步服务器

| NTP Server          | Description          |
| ------------------- | -------------------- |
| `cn.pool.ntp.org`   | NTP官方中国区        |
| `asia.pool.ntp.org` | NTP官方亚洲区        |
| `pool.ntp.org`      | NTP官方              |
| `ntp.sjtu.edu.cn`   | 上海交通大学网络中心 |

#### 二、插件库

| 名称                                                         | 插件库                                  | 说明                                                         |
| ------------------------------------------------------------ | --------------------------------------- | ------------------------------------------------------------ |
| [`Kodinerds Addon Repo`](http://www.kodiplayer.cn/plugins/3040.html) | https://repo.kodinerds.net/             | 一款国外的Kodi插件库，作为官网插件的补充，可挑选自己喜欢的插件安装。 |
| `Super Repo`                                                 | http://srp.nu                           | [superrepo.kodi.jarvis.all-0.7.04.zip](./Jarvis/superrepo.kodi.jarvis.all-0.7.04.zip) |
| `ALiYun Addons Repo`                                         | https://mirrors.aliyun.com/xbmc/addons/ | 阿里云插件库                                                 |
| `Jellyfin Repo`                                              | https://kodi.jellyfin.org               | Jellyfin官方插件库                                           |
| `EMBY Repo`                                                  | http://kodi.emby.media/                 | EMBY官方插件库                                               |
| `OpenVPN Repo`                                               | http://troypoint.com/repo               | [service.vpn.manager_6.4.3.zip](./Jarvis/service.vpn.manager_6.4.3.zip) |
| `tinyMediaManager Repo`                                      | https://archive.tinymediamanager.org/   | 为Kodi、jellyfin、emby、Plex媒体服务器提供元数据。           |
| `BH1HUY on Github Repo`                                      | https://bh1huy.github.io/               |                                                              |

#### 三、插件

| Add-ons                                                      | 说明                                                         | 备注                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`Backup`](http://www.kodiplayer.cn/plugins/2975.html)       | 备份Kodi配置的插件                                           | 通过搜索的方式安装。点击“插件”-“搜索”，输入backup，找到该插件，点击安装。 |
| [**`OpenSubtitles`**](http://www.kodiplayer.cn/plugins/2957.html) | 大型的开放式字幕库，自称是最大的开放式字幕库，提供电影及剧集字幕，有约600万条字幕。<br/>需要在https://www.opensubtitles.org/zh上面注册个账号，并在插件里面填入账号密码才能使用（注册密码要有大小写、数字、特殊字符，并用邮箱激活）。 |                                                              |
| [`Shooter`](http://www.kodiplayer.cn/plugins/2979.html)      | 射手字幕插件；字幕来源自伪射手https://assrt.net/，有多达387160个字幕。 |                                                              |
| [`Zimuku`](http://www.kodiplayer.cn/plugins/2932.html)       | 字幕库插件；字幕资源来自字幕库http://zmk.pw，含有以前射手网的字幕，新老字幕都非常多。因为是索引字幕库网站资源，网站程序变更、防御升级都可能造成插件无法使用。无法下载字幕的话请等待插件作者更新，或者到字幕库网站上手动下载字幕。<br>字幕库插件有两款，分别是taxigps制作的zimuku，pizzamx制作的zimukux，可选择使用。 |                                                              |
| `assrt.net`                                                  | 字幕                                                         |                                                              |
| [`Unlock Kodi Advanced Settings`](http://www.kodiplayer.cn/plugins/3003.html) | 让你免于敲打代码的烦恼，使用它就能在Kodi软件内进行更多的设置，设置内容会自动写入advancedsettings.xml |                                                              |
| [**`PVR IPTV Simple Client`**](http://www.kodiplayer.cn/plugins/2969.html) | 支持m3u播放列表、多播/单播源的直播电视流、收听广播频道和EPG，安装该插件可实现在Kodi上看电视。 |                                                              |
| **`gismeteo`**                                               | 天气预报                                                     |                                                              |
| [`IPTV Recorder`](http://www.kodiplayer.cn/plugins/2988.html) | 可实现录制Kodi电视直播的m3u8源，将电视播放节目录制保存到本地。还能定时录制，到点自动录制，方便回家观看。 |                                                              |
| [**`Jellyfin`**](http://www.kodiplayer.cn/plugins/2936.html) | Jellyfin是在Emby的基础上单独开发，Emby的硬件转码、客户端播放等功能需要付费，Jellyfin是完全免费的。<br>可以利用Kodi的Jellyfin插件来实现海报墙、播放记录的同步。配合Kodi来使用效果非常不错，大大增加Kodi的使用体验。 | 数据源                                                       |
| [`Emby`](http://www.kodiplayer.cn/plugins/2894.html)         | 一款类似Plex的媒体服务平台，统一管理视频音乐照片等多媒体文件，它有最强大的影片搜刮能力，并且可以非常便捷远程维护其媒体库。<br>Emby客户端解码转码使用的是服务器资源，不如Kodi作为播放器解码更强。而且Emby硬件转码收费，手机客户端收费，使用Emby for Kodi插件能绕过收费。Emby插件可让您直接在Kodi中浏览和播放Emby服务器中的媒体文件。<br>Emby需要设置一个服务器端(在存放电影文件的设备上安装)，支持windows、nas、linux、mac等。下载地址：https://emby.media/download.html | 数据源                                                       |
| **[`tinyMediaManager`](http://www.kodiplayer.cn/course/2945.html)** | 用Java/Swing编写的媒体管理工具，能够为Kodi、jellyfin、emby、Plex媒体服务器提供元数据。tinyMediaManager的原理是根据文件的标题到电影资料网站上匹配电影信息，下载电影的资料及图片到本地上，供Kodi、jellyfin、emby、plex等多媒体软件使用。<br/>建议下载version 3.x系列，version 4.x免费版只能管理50部。<br/>推荐选择刮削源为“themoviedb.org”（有片名、介绍的中文翻译）；近期themoviedb服务器经常无法连接，修改域名解析可解决。访问https://dnschecker.org/#A/api.themoviedb.org 及https://dnschecker.org/#A/image.themoviedb.org 查询国内可用IP。找到电脑C:\Windows\System32\drivers\etc\hosts文件，编辑添加IP记录，例如：<br/>52.222.158.31 image.tmdb.org<br/>52.222.174.75 api.tmdb.org | 数据源                                                       |

---

#### [插件库镜像更新发布地址](http://blog.sina.com.cn/s/blog_65637f130102yx9i.html)

##### 背景

近期，因为众所周知的原因，Kodi用户无法连接到官方插件库进行插件更新，因此，我尝试寻找国内可供更新的镜像源，然后找到国内有4家开源镜像站点提供Kodi官方镜像，因此，写了插件来供大家用于替换官方插件库。

##### 说明

1. 本插件是一个库，提供官方插件库在国内的4个开源站的镜像下载，这些镜像站点每日同步官方库中全部插件内容。通过本插件库，在中国无法连接官方插件库时，可以实现官方库中所有插件的安装及更新，可以完整取代官方插件库（即Kodi Add-on Repository）。
2. 请自行根据Kodi主程序的版本从四个镜像站点任选其一安装即可，无需安装多个。以下是关于文件名的说明：
   - 文件名中带leia的用于Kodi主程序v18.x
   - 文件名中带krypton的用于Kodi主程序v17.x
   - cnnic：从中国互联网络信息中心开源镜像站更新
   - nju：从南京大学开源镜像站更新
   - thu：从清华大学开源镜像站更新
   - ustc：从中国科学技术大学开源镜像站更新
3. 官方插件库中没有的插件当然也就无法通过这些镜像站安装和更新，非官方插件库中的插件有任何问题也无法通过这个插件解决。
4. 如何离线安装插件请[查阅](http://blog.sina.com.cn/s/blog_65637f130102yx9j.html)
5. 有任何问题请在这篇博文下[留言反馈](http://blog.sina.com.cn/s/blog_65637f130102yx9i.html)

##### 可解决的近期问题

- 无法切换中文语言界面，详细[解决办法](http://blog.sina.com.cn/s/blog_65637f130102yx9l.html)
- 无法更新官方插件
- 因使用官方刮削器插件而出现的无法刮削的问题

##### 更新日志

- [B]Version 0.0.2[/B]

  - 将安装源从HTTP模式切换至HTTPS模式.
  - 更新插件描述.
  - 更改图标为官方库图标.
  - [B]Version 0.0.1[/B]
  - 创建本项目.

---

**下载链接**：https://pan.baidu.com/s/1P8BD_nkOLvFFP61E2__cdQ 提取码：r92g
