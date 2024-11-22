# 虚幻引擎源码编译与项目打包安卓过程记录

## 源码下载

UE源码地址：[EpicGames/UnrealEngine: Unreal Engine source code](https://github.com/EpicGames/UnrealEngine)

在下载源码之前，要将自己Epic账号与GitHub账号相关联

UE官网：[最强大的实时3D创作工具 - Unreal Engine](https://www.unrealengine.com/zh-CN)

账号关联好之后，从本地拉取UE源码：

```git
git clone https://github.com/EpicGames/UnrealEngine
```

也可以直接下载项目相应版本的压缩包(这下载更快一点)

然后进入项目根目录，运行**Setup.bat**下载项目依赖包。

之后再运行**GenerateProjectFiles.bat**。运行完之后，根目录会多出UE5.sln。

## 源码编译

用Visual studio打开项目根目录的UE.sln文件，打开之后会发现vs报了很多漏洞错误，**不要去管它**。

之后**右键**点击UE5将其设为启动项目。

![image1](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image1.png)

再将win64旁边的选项改为Development Editor

![image2](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image2.png)

最后点击绿色三角开始编译（编译时间会有点久，建议硬盘空间保留至少150G）

## 项目打包安卓

编译完成后会自动打开UnrealEditor(该可执行文件位与Engine\Binaries\Win64下),随便新建一个项目，进行简单工程设置和场景编辑。

### jdk,sdk和ndk下载

在打包安卓之前，要先进行环境设置，**下载jdk,sdk和ndk**。

根据UE官网建议下载对应的版本（[虚幻引擎Android开发要求 | 虚幻引擎 5.4 文档 | Epic Developer Community | Epic Developer Community](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/android-development-requirements-for-unreal-engine?application_version=5.4)）。

![image3](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image3.png)

- **下载Android Studio**

官网：https://developer.android.com/studio?hl=zh-cn

- **下载jdk-17.0.6**

 官网：https://www.oracle.com/hk/java/technologies/downloads/

- **SDK和NDK下载**

安装好Android Studio并打开，进入设置界面，找到Android SDK中的SDK Tools

![image4](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image4.png)

选择33版本的SDK和25版本的NDK下载。

### 配置系统环境变量

上面的都下载完成后，**开始配置系统环境变量**。

- **ANDROID_HOME**：SDK的下载目录。
- **JAVA_HOME**：JDK的下载目录。
- **NDK_ROOT/NDKROOT**：NDK下载目录，一般在SDK下载目录下。

不配置系统环境变量的话，也可以在UE的**项目设置/平台/Android SDK**里指定JDK,SDK,NDK。

![image5](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image5.png)

### 项目设置

环境配置好了以后，**进行项目设置**

打开要打包的项目，进入**项目设置/平台/Android**。

![image6](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image6.png)

点击**立即配置**

![image7](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image7.png)

设置App名字

![image8](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image8.png)

勾上该选项

![image9](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image9.png)

点击**立即配置**

### 开始打包

上述操作做完后就可以开始打包。

根据下面的步骤进行打包。

![image10](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image10.png)

打包完成后后生成下面的这些文件。将其中的**项目名-arm64.apk**文件传输到手机上下载安装就可以运行。

![image11](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image11.png)

安卓手机运行成功示例

![image14](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image14.jpg)

### 打包过程中遇到的一些问题

![image12](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image12.png)

如果箭头所指的位置显示**TurnKey返回错误代码1**，并且点击打包项目会**弹窗提示未下载SDK**的话，这个问题我也不知道为什么，可能是因为编译源码时看到报错忍不住给源码更换了更高版本的包导致的问题吧（我就是这么干了）。

解决这个问题的话，我是重新下载源码并编译，然后就没出现这个问题了。

![image13](https://raw.githubusercontent.com/Elysia125/UESourceCode_compilation-and-packaging_Android/main/images/image13.png)

如果打包过程中出现上述报错（好像是什么证书问题）导致打包失败，可以打开路径**C:\Users\用户\.gradle\wrapper\dists\gradle-版本号-all\文件名**删除该路径下的所有文件，然后进入打包过程中要下载的文件的官网[Gradle | Releases](https://gradle.org/releases/)下载相应版本的压缩包文件，将该文件放入**C:\Users\用户\.gradle\wrapper\dists\gradle-版本号-all\文件名**目录下。
