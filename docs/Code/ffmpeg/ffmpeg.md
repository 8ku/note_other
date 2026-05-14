# ffmpeg

1. [下载](https://www.ffmpeg.org/download.html)
2. 解压
3. 使用



## 常用命令

### 转换格式

* To **Mp4**: `ffmpeg -i input.mov output.mp4`

* Mp4 to **mp3**: `ffmpeg -i input.mp4 -b:a 192k -vn output.mp3`



### 压缩

* **Video**: `ffmpeg -i input.mp4 -vcodec h264 -acodec aac output.mp4`
* **Audio**(compress to 96k): `ffmpeg -i input.mp4 -b:a 96k -map a out.mp3`



## 裁剪长度

* `ffmpeg -ss startSec -i input.mp4 -t length output.mp4`



## yt-dlp

### Download

* **Audio** Only: `yt-dlp -x “url”`
