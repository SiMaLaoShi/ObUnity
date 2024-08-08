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


## 切割VSF

```python
def split_unityfs_file(src_file_path):  
    # 二进制标识符，UnityFS的UTF-8编码  
    unityfs_marker = b'UnityFS'  
  
    # 打开原始二进制文件进行读取  
    with open(src_file_path, 'rb') as file:  
        file_content = file.read()  
  
    # 查找所有的UnityFS标识符位置  
    marker_indices = []  
    index = file_content.find(unityfs_marker)  
    while index != -1:  
        marker_indices.append(index)  
        index = file_content.find(unityfs_marker, index + 1)  
  
    # 分割原始二进制文件并写入新的文件  
    for i, start_idx in enumerate(marker_indices):  
        # 决定分割部分的结束位置  
        end_idx = marker_indices[i + 1] if i + 1 < len(marker_indices) else None  
        part = file_content[start_idx:end_idx]  
  
        # 写入分割后的文件  
        with open(f"split_part_{i}.unityfs", 'wb') as split_file:  
            split_file.write(part)  
  
  
if __name__ == '__main__':  
    # 使用函数并传入源文件路径  
    split_unityfs_file(r'')
```