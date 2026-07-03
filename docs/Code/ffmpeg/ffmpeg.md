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
   for %i in (*.mp3) do ffmpeg -i "%i" -vn -c:a aac -b:a 192k "%~ni.m4b"
   ```
   1.1 Speed this process

   Check if your file is AAC:

   ```cmd
   ffprobe -v error -select_streams a:0 -show_entries stream=codec_name -of default=noprint_wrappers=1:nokey=1 "output.m4b"
   ```

   If it is, the just copy it, skip re-encoding: 

   ```cmd
   ffmpeg -f concat -safe 0 -i list.txt -i chapters.txt -map 0 -map_metadata 1 -c copy "output.m4b"
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
   import sys
   import re
   
   # 设置 UTF-8（Windows）
   if sys.platform == 'win32':
       try:
           sys.stdout.reconfigure(encoding='utf-8')
       except AttributeError:
           pass
   
   # 获取所有 m4b 文件（排除最终输出文件）
   files = sorted([f for f in os.listdir('.') if f.endswith('.m4b') and f != 'Odyssey.m4b' and f != 'Troy.m4b'])
   
   if not files:
       print("❌ 没有找到 .m4b 文件")
       sys.exit(1)
   
   print(f"找到 {len(files)} 个文件:\n" + "\n".join(f"  - {f}" for f in files))
   print("-" * 50)
   
   metadata = [';FFMETADATA1\n\n']
   start_ms = 0
   used_titles = set()
   chapter_count = 0
   
   for idx, f in enumerate(files, 1):
       print(f"[{idx}/{len(files)}] 处理: {f}")
       
       # 运行 ffprobe 获取信息
       probe = subprocess.run([
           'ffprobe', '-v', 'quiet',
           '-print_format', 'json',
           '-show_format', '-show_chapters', f
       ], capture_output=True)
       
       if probe.returncode != 0:
           print(f"  ⚠️ 警告：无法读取文件，跳过")
           print(f"  错误: {probe.stderr.decode('utf-8', errors='ignore')[:200]}")
           continue
       
       # 解码输出
       try:
           output = probe.stdout.decode('utf-8')
       except UnicodeDecodeError:
           output = probe.stdout.decode('gbk', errors='ignore')
       
       # 解析 JSON
       try:
           data = json.loads(output)
       except json.JSONDecodeError as e:
           print(f"  ⚠️ JSON 解析失败: {e}")
           continue
       
       # 获取音频时长
       duration_ms = int(float(data['format']['duration']) * 1000)
       
       # 获取文件的元数据标题
       format_tags = data['format'].get('tags', {})
       file_title = format_tags.get('title', '')
       
       # 如果文件标题为空，尝试从文件名提取
       if not file_title:
           raw = f.replace('.m4b', '').replace('.mp3', '')
           # 去掉开头的数字和分隔符
           file_title = re.sub(r'^[\d\s\-_]+', '', raw)
           if not file_title:
               file_title = f"Chapter {idx}"
       
       # 获取章节信息
       chapters = data.get('chapters', [])
       
       if chapters:
           # ========== 情况1：文件有内部章节 ==========
           print(f"  ✓ 发现 {len(chapters)} 个内部章节")
           for ch in chapters:
               s = int(float(ch['start_time']) * 1000) + start_ms
               e = int(float(ch['end_time']) * 1000) + start_ms
               
               # 从章节标签获取标题，如果没有则使用文件标题
               ch_tags = ch.get('tags', {})
               title = ch_tags.get('title', '')
               
               # 如果章节标题为空，使用文件标题 + 章节编号
               if not title:
                   title = f"{file_title} - Part {len(chapters) if len(chapters) > 1 else ''}"
                   if len(chapters) > 1:
                       title = f"{file_title} - Part {chapters.index(ch) + 1}"
               
               # 确保标题唯一
               if title in used_titles:
                   title = f"{title} ({chapters.index(ch) + 1})"
               used_titles.add(title)
               
               metadata.append(f'[CHAPTER]\nTIMEBASE=1/1000\nSTART={s}\nEND={e}\ntitle={title}\n\n')
               chapter_count += 1
       else:
           # ========== 情况2：文件没有内部章节 ==========
           print(f"  ✓ 无内部章节，使用文件标题: '{file_title}'")
           
           # 确保标题唯一
           if file_title in used_titles:
               file_title = f"{file_title} ({idx})"
           used_titles.add(file_title)
           
           metadata.append(f'[CHAPTER]\nTIMEBASE=1/1000\nSTART={start_ms}\nEND={start_ms + duration_ms}\ntitle={file_title}\n\n')
           chapter_count += 1
       
       start_ms += duration_ms
       print(f"    当前总时长: {start_ms // 3600000}h {(start_ms % 3600000) // 60000}m")
   
   # 写入元数据文件
   with open('chapters.txt', 'w', encoding='utf-8') as mf:
       mf.writelines(metadata)
   
   print("-" * 50)
   print(f"✅ 生成完成!")
   print(f"   - 处理文件数: {len(files)}")
   print(f"   - 生成章节数: {chapter_count}")
   print(f"   - 总时长: {start_ms // 3600000}h {(start_ms % 3600000) // 60000}m {(start_ms % 60000) // 1000}s")
   print(f"   - 输出文件: chapters.txt")
   print("\n📝 预览前 5 个章节:")
   for i, line in enumerate(metadata[1:11]):  # 跳过 FFMETADATA 头，显示前 10 行
       if line.strip():
           print(f"  {line.strip()}")
       if i >= 9:
           break
   
   print("\n🚀 run this:")
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

   5.1 Skip re-encoding, add cover image:

   ```cmd
   ffmpeg -i input.m4b -i cover.jpg -map 0:a -map 1:v -c:a copy -c:v copy -disposition:v attached_pic -metadata:s:v title="Album cover" -metadata:s:v comment="Cover (front)" output_cover.m4b
   ```
   
   
   
   







# yt-dlp

## Download

* **Audio** Only: `yt-dlp -x “url”`
