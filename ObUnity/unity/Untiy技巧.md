## 自动属显示在Inspector上

```C#
internal class Pay : MonoBehaviour  
{  
    private string payProduct = string.Empty;  
  
    public string stringField = "this is string ";  
    
	//添加上这个就可以序列化在检视面板上了
    [field: SerializeField] public string stringAutoProperty { get; set; }
}
```

添加上 [field: SerializeField] 就可以了

## 创建游戏对下默认在零点

![[Pasted image 20240430145809.png]]

## 打开Unity内置的DeveloperMode

```C#
private const string k_DeveloperMode = "DeveloperMode";  
  
[MenuItem(MenuKey.DEVELOPER_MODE)]  
private static void DeveloperMode()  
{  
    var bDeveloperMode = EditorPrefs.GetBool(k_DeveloperMode, false);  
    EditorPrefs.SetBool(k_DeveloperMode, !bDeveloperMode);  
    Menu.SetChecked(MenuKey.DEVELOPER_MODE, bDeveloperMode);  
}  
  
[MenuItem(MenuKey.DEVELOPER_MODE, true)]  
private static bool DeveloperModeEnabled()  
{  
    var bDeveloperMode = EditorPrefs.GetBool(k_DeveloperMode, false);  
    Menu.SetChecked(MenuKey.DEVELOPER_MODE, bDeveloperMode);  
    return true;  
}
```

## 粒子在Scene面板一直播放，不需要选中

![[Pasted image 20240430152905.png]]

## 自动属显示在Inspector上

```C#
internal class Pay : MonoBehaviour  
{  
    private string payProduct = string.Empty;  
  
    public string stringField = "this is string ";  
    
	//添加上这个就可以序列化在检视面板上了
    [field: SerializeField] public string stringAutoProperty { get; set; }
}
```

添加上 [field: SerializeField] 就可以了

## 创建游戏对下默认在零点

![[Pasted image 20240430145809.png]]

## 打开Unity内置的DeveloperMode

```C#
private const string k_DeveloperMode = "DeveloperMode";  
  
[MenuItem(MenuKey.DEVELOPER_MODE)]  
private static void DeveloperMode()  
{  
    var bDeveloperMode = EditorPrefs.GetBool(k_DeveloperMode, false);  
    EditorPrefs.SetBool(k_DeveloperMode, !bDeveloperMode);  
    Menu.SetChecked(MenuKey.DEVELOPER_MODE, bDeveloperMode);  
}  
  
[MenuItem(MenuKey.DEVELOPER_MODE, true)]  
private static bool DeveloperModeEnabled()  
{  
    var bDeveloperMode = EditorPrefs.GetBool(k_DeveloperMode, false);  
    Menu.SetChecked(MenuKey.DEVELOPER_MODE, bDeveloperMode);  
    return true;  
}
```

## 粒子在Scene面板一直播放，不需要选中

![[Pasted image 20240430152905.png]]

Simulate Layers选Evertting就行了

## IOS提审被崩溃被打回的日志文件还原

把日志文件改为.crash文件然后后用xcode打开，选择对应工程就能还原崩溃信息

## Pod修改Other Link 

由于pod install 会修改OTHER_LDFLAGS，导致一些问题，可以直接用pod的处理来操作

```lua
post_install do |installer|
  installer.pods_project.targets.each do |target|
    if target.name == 'Pods-Unity-iPhone'
      puts "Found Unity-iPhone target, updating OTHER_LDFLAGS..."
      
      target.build_configurations.each do |config|
        xcconfig_path = config.base_configuration_reference.real_path
        puts "Updating xcconfig file: #{xcconfig_path}"
        xcconfig = File.read(xcconfig_path)
        # 修改OTHER_LDFLAGS行
        xcconfig.gsub!(/^OTHER_LDFLAGS = .*\n/, "OTHER_LDFLAGS = -ObjC\n")
        # 写回xcconfig文件
        File.write(xcconfig_path, xcconfig)
        
        puts "OTHER_LDFLAGS updated successfully."
      end
    end
  end
end
```