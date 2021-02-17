# FFMPEG

使用ffmpeg对多媒体文件进行操作

## 常用方法

### 截取视频片段

使用 `-ss [time] -t [length] -c copy` 来快速裁剪视频

e.g.

截取一段从1分钟开始，长度为8分42秒的视频内容

```bash
▶ ffmpeg -ss 00:01:00 -t 00:08:42 -c copy output.mp4
```





### 使用concat合并文件

e.g.

需要合并的文件：`slice1.mp4`, `slice2.mp4`

新建文档 `list.txt`，并输入以下内容进行保存

```txt
file 'slice1.mp4'
file 'slice2.mp4'
```

使用指令快速合并

```bash
▶ ffmpeg -f concat -i list.txt -c copy output.mp4
```



## 指令

用法：

`ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfle}...`

参数：

+ `-version`

  查看当前ffmpeg版本以及其他信息，由于ffmpeg是编译的时候选择性组件进行编译的，因此是否能使用某些功能还得看当前ffmpeg是否包含了相应组件，由于是开源的，甚至可以自己写一个自定义组件

  ```shell
  ▶ ffmpeg -version
  # 版本号
  ffmpeg version 4.3.1-tessus  https://evermeet.cx/ffmpeg/  Copyright (c) 2000-2020 the FFmpeg developers
  built with Apple clang version 11.0.0 (clang-1100.0.33.17)
  # 配置以及包含的功能库
  configuration: --cc=/usr/bin/clang --prefix=/opt/ffmpeg --extra-version=tessus --enable-avisynth --enable-fontconfig --enable-gpl --enable-libaom --enable-libass --enable-libbluray --enable-libdav1d --enable-libfreetype --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libmysofa --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenh264 --enable-libopenjpeg --enable-libopus --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvmaf --enable-libvo-amrwbenc --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxavs --enable-libxvid --enable-libzimg --enable-libzmq --enable-libzvbi --enable-version3 --pkg-config-flags=--static --disable-ffplay
  libavutil      56. 51.100 / 56. 51.100
  libavcodec     58. 91.100 / 58. 91.100
  libavformat    58. 45.100 / 58. 45.100
  libavdevice    58. 10.100 / 58. 10.100
  libavfilter     7. 85.100 /  7. 85.100
  libswscale      5.  7.100 /  5.  7.100
  libswresample   3.  7.100 /  3.  7.100
  libpostproc    55.  7.100 / 55.  7.100
  
  ```

+ `-codecs`

  查看当前支持的编码器

  ```shell
  ▶ ffmpeg -codecs
  ffmpeg version 4.3.1-tessus  https://evermeet.cx/ffmpeg/  Copyright (c) 2000-2020 the FFmpeg developers
    built with Apple clang version 11.0.0 (clang-1100.0.33.17)
    configuration: --cc=/usr/bin/clang --prefix=/opt/ffmpeg --extra-version=tessus --enable-avisynth --enable-fontconfig --enable-gpl --enable-libaom --enable-libass --enable-libbluray --enable-libdav1d --enable-libfreetype --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libmysofa --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenh264 --enable-libopenjpeg --enable-libopus --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvmaf --enable-libvo-amrwbenc --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxavs --enable-libxvid --enable-libzimg --enable-libzmq --enable-libzvbi --enable-version3 --pkg-config-flags=--static --disable-ffplay
    libavutil      56. 51.100 / 56. 51.100
    libavcodec     58. 91.100 / 58. 91.100
    libavformat    58. 45.100 / 58. 45.100
    libavdevice    58. 10.100 / 58. 10.100
    libavfilter     7. 85.100 /  7. 85.100
    libswscale      5.  7.100 /  5.  7.100
    libswresample   3.  7.100 /  3.  7.100
    libpostproc    55.  7.100 / 55.  7.100
  Codecs:
   D..... = Decoding supported
   .E.... = Encoding supported
   ..V... = Video codec
   ..A... = Audio codec
   ..S... = Subtitle codec
   ...I.. = Intra frame-only codec
   ....L. = Lossy compression
   .....S = Lossless compression
   -------
   D.VI.S 012v                 Uncompressed 4:2:2 10-bit
   D.V.L. 4xm                  4X Movie
   D.VI.S 8bps                 QuickTime 8BPS video
   .EVIL. a64_multi            Multicolor charset for Commodore 64 (encoders: a64multi )
   .EVIL. a64_multi5           Multicolor charset for Commodore 64, extended with 5th color (colram) (encoders: a64multi5 )
   D.V..S aasc                 Autodesk RLE
   D.V.L. agm                  Amuse Graphics Movie
   D.VIL. aic                  Apple Intermediate Codec
   DEVI.S alias_pix            Alias/Wavefront PIX image
   DEVIL. amv                  AMV Video
   D.V.L. anm                  Deluxe Paint Animation
   D.V.L. ansi                 ASCII/ANSI art
   DEV..S apng                 APNG (Animated Portable Network Graphics) image
  # etc...
  
  ```

  可以配合使用 `grep [keywords]` 来快速查看是否支持某种格式

+ `-formats`

  查看支持的文件格式

+ `-i [file]`

  指定 input 输入文件，可以是多媒体问题件，也可以是一个包含参数的配置文件

+ `-ss [time]`

  指定开始时间 e.g. `-ss 00:01:00`

+ `-t [time]`

  指定时长 e.g `-t 00:08:00` 

+ `-c/codec [codec name]`

  指定音频和视频编码器，若使用`-c copy` 则不变,速度最快， e.g. `-c hevc`

+ `-vcodec [codec name]`

  指定视频编码器

+ `-acodec [codec name]`

  指定音频编码器

+ `-f [fmt]`

  强制格式

+ `-y`

  若输出文件已存在，则不询问直接覆盖

+ `-max_muxing_queue_size [numeric]`

  设置缓存大小 e.g. `-max_muxing_queue_size 1024`

+ `-s [size]`

  指定分辨率 e.g. `-s 1280x720`



## 常见问题

+ `Unsafe file name '切片（上半部分）.mp4'`

  不安全名称，请使用全英文