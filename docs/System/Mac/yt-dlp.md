# yt-dlp

[Github Link](https://github.com/yt-dlp/yt-dlp)



### 下载最高质量的视频

```bash
yt-dlp --output "%(title)s.%(ext)s" --embed-thumbnail --add-metadata --merge-output-format mp4 "url"
```



### 列出字幕

```bash
	yt-dlp --list-subs "url"
```



### 下载视频和字幕 

```bash
yt-dlp --output "%(title)s.%(ext)s" --sub-lang zh-TW --write-sub --convert-subs srt --embed-thumbnail --add-metadata --merge-output-format mp4 "url
```

