
## 步骤 1: 创建空目录

在命令行中执行以下命令，创建一个新的空目录以作为工程目录：

```bash
mkdir MyNewProject
cd MyNewProject
```

## 步骤 2: 找到合适的 `gradle.bat`

确保您已安装Gradle，并找到以下路径中的 `gradle.bat` 文件：

```sh
.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\bin\gradle.bat

```


## 步骤 3: 初始化工程目录

在命令行中使用找到的 `gradle.bat` 文件初始化工程：

## 步骤 4: 新建模块目录

在新创建的工件目录中创建一个名为 `myModule` 的子目录，并设置如下的目录结构：

```sh
MyNewProject/
└── myModule/
    ├── libs/
    └── src/
```


## 步骤 5:添加 JAR 文件

将所需的 JAR 文件放入到 `libs` 文件夹中。这些库将被 Gradle 构建系统自动编译与打包。

```sh
MyNewProject/
└── myModule/
    ├── libs/
	    ├── mylibrary1.jar
	    ├── mylibrary2.jar
    └── src/
```

## 步骤 6:修改模块的 `build.gradle`

在 `myModule` 目录下，修改模块的 `build.gradle` 文件，确保它包含以下内容：
```sh
// MyLibrary/myModule/build.gradle (模块级)
apply plugin: 'com.android.library'

android {
    compileSdkVersion 30
    defaultConfig {
        minSdkVersion 16
        targetSdkVersion 30
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
}

```

## 步骤7: 添加模块到项目

修改根项目的 `settings.gradle` 文件，以便将新模块 `slib` 添加到项目中。确保文件中包含以下内容：
```sh
include ':slib'
```

## 步骤8: 生成项目

1. 回到项目根目录，使用以下命令生成项目：
```sh
gradlew.bat build
```
2. 确保没有错误后，您的模块应该成功集成到工程中。