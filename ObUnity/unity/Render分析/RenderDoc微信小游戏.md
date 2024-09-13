
## 准备工具

- [Renderdoc最新版本](https://renderdoc.org/)
- [MuMu12最新版本](https://mumu.163.com/)

## 设置

### Mumu模拟器设置

- Mumu12选Vulkan

设置完记得重启，任务管理器里面看看有没有其他的Mumu进程，都杀掉

### Renderdoc设置![[RenderDoc分析Webgl#Renderdoc设置]]
**File > Launch Application**

![[Pasted image 20240910151310.png]]

![[Pasted image 20240910151013.png]

- **Executable Fath** ：选择你安装的Mumu里面的路径 **D:\MuMu12\MuMuPlayer-12.0\shell\MuMuPlayer.exe**
- **Working Directory** ：这个会自动设置
- **Enable Global Hook** ：这个开启设置完路径大概是这个样子

![[Pasted image 20240910151323.png]]

启动Mumu模拟器，如果你在设置之前已经启动那就重启。

等进入到Mumu成功的话，会有RenderDoc的标识。

![[Pasted image 20240910151433.png]]

### 调试

**File > Attach to Ruing Instance**

![[Pasted image 20240910151818.png]]

选择MumuVMMHeadless

Connect to App就基本完成了

### 小游戏截帧

微信里面启动小游戏，就可以截帧了。