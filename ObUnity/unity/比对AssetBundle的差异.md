## 步骤1：找到WebExtract

找到WebExtract，这个一般在Unity的安装目录，当然前提你得你AssetBundle的的什么Unity版本，这里的WebExtract在这个目录。
```sh
D:\Uni\20210346\Editor\Data\Tools\WebExtract.exe
```

## 步骤2：解压AssetBundle

使用WebExtract解压AssetBundle

```sh
WebExtract.exe char_default_3
```

解压出来会有这这个目录 char_default_3_data，里面会包含一个CAB-xxxx的文件

## 步骤3：获取匹配版本的binary2text

找到binary2text.exe，也是在Unity的安装目录

```sh
D:\Uni\20210346\Editor\Data\Tools\binary2text.exe
```

## 步骤4：把AssetBundle转为text

```sh
binary2text.exe CAB-xxx
```

最终会生成一个同名的txt文件，就可以对比了