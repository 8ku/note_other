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



### 裁剪长度

* `ffmpeg -ss startSec -i input.mp4 -t length output.mp4`



### Convert mp3s to audiobook format

1. Convert each mp3 file to m4b file:

   ```cmd
   for %i in (*.mp3) do ffmpeg -i "%i" -vn -c:a aac -b:a 192k "%~ni.m4b"`
   ```

2. Create list of those m4b files: 

   ````cmd
   for %f in (*.m4b) do @echo file '%~f' >> list.txt
   ````

3. Run python script to create chapter list

   ```python
   import subprocess
   import json
   import os
   
   # Get all m4b files sorted
   files = sorted([f for f in os.listdir('.') if f.endswith('.m4b') and f != 'input.m4b'])
   
   metadata = [';FFMETADATA1\n\n']
   start_ms = 0
   
   for f in files:
       # Get duration
       probe = subprocess.run([
           'ffprobe', '-v', 'quiet',
           '-print_format', 'json',
           '-show_format', '-show_chapters', f
       ], capture_output=True, text=True)
       
       data = json.loads(probe.stdout)
       duration_ms = int(float(data['format']['duration']) * 1000)
       chapters = data.get('chapters', [])
   
       if chapters:
           for ch in chapters:
               s = int(float(ch['start_time']) * 1000) + start_ms
               e = int(float(ch['end_time']) * 1000) + start_ms
               title = ch['tags'].get('title', f.replace('.m4b', ''))
               metadata.append(f'[CHAPTER]\nTIMEBASE=1/1000\nSTART={s}\nEND={e}\ntitle={title}\n\n')
       else:
           # No chapters in file, use filename as chapter title
           title = f.replace('.m4b', '').lstrip('0123456789 -')
           metadata.append(f'[CHAPTER]\nTIMEBASE=1/1000\nSTART={start_ms}\nEND={start_ms + duration_ms}\ntitle={title}\n\n')
   
       start_ms += duration_ms
   
   # Write metadata file
   with open('chapters.txt', 'w', encoding='utf-8') as mf:
       mf.writelines(metadata)
   
   # Write file list
   with open('list.txt', 'w', encoding='utf-8') as lf:
       for f in files:
           lf.write(f"file '{f}'\n")
   
   print("Generated list.txt and chapters.txt")
   print(f"Total duration: {start_ms // 3600000}h {(start_ms % 3600000) // 60000}m")
   print("Now run:")
   print('ffmpeg -f concat -safe 0 -i list.txt -i chapters.txt -map_metadata 1 -c copy "output.m4b"')
   ```

4. Merge them to one m4b file: 

   ```cmd
   ffmpeg -f concat -safe 0 -i list.txt -i chapters.txt -map 0 -map_metadata 1 -c:a aac -b:a 192k "Mythos.m4b"
   ```

5. Add cover image:

   ```cmd
   ffmpeg -i input.m4b -i Mythos.jpg -map 0:a -map 1:v -c:a copy -c:v mjpeg -disposition:v attached_pic -metadata:s:v title="Album cover" -metadata:s:v comment="Cover (front)" Mythos_cover.m4b
   ```

   

   







# yt-dlp

## Download

* **Audio** Only: `yt-dlp -x “url”`
