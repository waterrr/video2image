# video2image

实现把视频分片并上传到阿里云图床并且自动生产m3u8文件

目前来说，还是没啥问题的，但是请不要滥用阿里图床。

研究发现，阿里上传接口没有做图片检测处理，所以可以把一段视频切成很多段ts文件，然后以jpg后缀上传到阿里服务器。

演示网址：https://www.gksec.com/github_demo/video2image.html

![20200227161737.png](https://pic.downk.cc/item/5e5780026127cc0713fa6fbd.png)



## [go-video2image.exe](https://github.com/waterrr/video2image/blob/master/go-video2image.exe)

Windows版本，已经编译好，直接下载即可使用。

版权由[Dxkite](https://github.com/dxkite)所有，禁止商业行为。

**Usage**

```
Usage of go-video2image.exe:
  -bin string
        ffmpeg binary command (default "ffmpeg")
  -ext string
        image extension (default "jpg")
  -help
        the file name be input
  -input string
        the mp4 file
  -output string
        the output m3u8 index (default "output.m3u8")
  -temp string
        the template dir (default "tmp")
  -time int
        time per segment (default 30)
  -type string
        the type to upload image (default "ali")
```

上面看不明白不要紧，还支持傻瓜操作，直接把视频拖进去，默认每段30s,如果运行到一半闪退了，那么说明切割的视频每30s大于5M，无法上传，这时候你需要简单计算一下，把每段视频都控制到5MB大小以内，然后用cmd执行。

```
go-video2image.exe -input xxx.mp4 -time 15
```

其中-time后面的参数请自行调整，只要切片保持在5MB以内就行了。

运行完成后出现`main.go:63: success`字样就说明成功了，你会发现文件夹内多出了output.m3u8，这就是你需要的文件，tmp文件夹为切片临时文件，可以删除。

**需要注意的地方**

1. 视频切片基于ffmpeg，请先下载好ffmpeg.exe(请自行下载)和需要处理的视频放在同一目录。
2. 每段切片请务必小于5MB，这是阿里上传接口限制的。

