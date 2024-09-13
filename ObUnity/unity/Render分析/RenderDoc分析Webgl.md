
## 准备工具

[RenderDoc1.13](https://renderdoc.org/stable/1.13/RenderDoc_1.13_64.zip)

[chrome](https://www.google.com/intl/zh-CN/chrome/)

RenderDoc的最新版本不行，可以常试试一下，谷歌浏览器版本无所属
RenderDoc的最新版本不行，可以常试试一下，谷歌浏览器版本无所属
RenderDoc的最新版本不行，可以常试试一下，谷歌浏览器版本无所属
## 截帧步骤

### Renderdoc设置

**Tools > Settings**

![[Pasted image 20240910122846.png]]

**Grneral > Allow globsl process hooking-be careful!** 

![[Pasted image 20240910122949.png]]

设置完需要重启RenderDoc

### 启动浏览器

```sh
C:\Windows\System32\cmd.exe /c "SET RENDERDOC_HOOK_EGL=0 && START "" "C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-gpu-sandbox --gpu-startup-dialog"
```

根据自己的路径调整一下，也可以写成bat，然后通过bat启动

启动浏览器会提示一个pid
![[Pasted image 20240910142035.png]]

暂时不用关闭，记录下这个pid有用的

### RenderDoc注入进程

**File > Inject into Process** 
如果忽略了第一步会没有这个选项

![[Pasted image 20240910142143.png]]

![[Pasted image 20240910142312.png]]

通过刚才记录的pid筛选到进程，Inject后。

![[Pasted image 20240910142605.png]]

这里的内容暂时是灰的，不能使用，别急。

回到我们的浏览器的，下面这个的提示确定后就行了。


![[Pasted image 20240910142354.png]]

这里确定就好了，回到RenderDoc。


![[Pasted image 20240910142459.png]]

确定之后刚刚这里的内容就可以使用了。

正常的话浏览器上就有RenderDoc的提示了

![[Pasted image 20240910142811.png]]

F12有冲突就使用RenderDoc到按钮使用