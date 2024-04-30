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