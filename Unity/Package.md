* TOC
{:toc}
## Cinemachine

### 第三人称跟随

- 下载导入包
- 顶部菜单栏 Cinemachine - Create Virtual camera
- 在角色下建一个空的子对象, 把子对象做为摄像机 follow 的对象
- Body - Damping 可以调整当角色移动多远时, 摄像机跟随 (Tutorial 里设置为 z:5)



## Controller

### Input System

- 在package manager中安装package
- 在需要控制的角色Inspector下添加 Player Input component(**这样会自动创建基本控制配置**)
  - Actions - Create Actions