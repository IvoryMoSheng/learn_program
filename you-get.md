You-get是一个很小的命令行工具，用来从网络下载媒体内容（视频、音频、图像）。

实现的功能：

*  从流行的网站下载视频/音频
*  使用本地媒体播放器播放在线视频，不用浏览器，没有广告
*  通过爬取一个网页来下载图片
*  下载任意非HTML内容（二进制文件）

安装需要的工具：

* Python 3
* FFmpeg (推荐) or Libav
* RTMPDump（可选）

---
安装步骤：

1.通过Python3版本的pip下载you-get

```
$ pip3 install you-get
```

2.更新you-get版本

```
$ pip3 install --upgrade you-get
```

3.-info/-i查看视频的格式质量

```
$ you-get -i [URL]
```

其中包含默认的视频格式，内嵌字幕同时被下载

想要下载其他格式，则根据You-get返回的信息进行配置

```
$ you-get --format=hd3 [URL]
```
4.ctrl+c暂停或恢复下载，可使用—-force参数强制重新下载，将覆盖原有的同名文件夹
5.使用--output-dir/-o设置下载路径，使用--output-filename/-O设置下载文件名
6.使用--url/-u查看站点可提取的资源,--json查看可爬取数据的JSON格式