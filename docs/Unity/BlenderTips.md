## In-Blender Python

### 在Blender中安装Python包（Windows）

1. 把代理设置到系统环境中
   1. 打开 `此电脑 - 属性 - 高级系统设置 - 环境变量 - 系统变量`
   2. 新增两个系统变量
      1. `http_proxy` : `socks5://127.0.0.1:xxxx`
      2. `https_proxy` : `socks5://127.0.0.1:xxxx`
2. 在Python中使用代理下载包
   1. 因为Python需要使用`pysocks5`包才能使用代理，先到 www.pypi.org 下载 `pysocks5`
   2. 找到Blender安装目录下的python.exe，一般在版本号内的 bin 文件夹中，把下载的pysocks5放到同级目录中
   3. 在当前文件夹打开CMD，运行 `.\python.exe -m pip install packagename`