## win10家庭版安装Docker

### 1. 开启Hyper-V

新建`hyperv.cmd`文件，内容如下：

```
pushd "%~dp0"

dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt

for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"

del hyper-v.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL
```

以管理员身份执行`hyperv.cmd`文件,然后重启。 
 在`控制面板->程序和功能->启用或关闭Windows功能`打开Hyper-V。

### 2. 伪装成win10专业版

以管理员身份打开cmd，执行如下命令：

```
REG ADD "HKEY_LOCAL_MACHINE\software\Microsoft\Windows NT\CurrentVersion" /v EditionId /T REG_EXPAND_SZ /d Professional /F
```

### 3. 下载Docker for Windows

官网下载链接（需FQ）： https://store.docker.com/editions/community/docker-ce-desktop-windows

国内镜像：
 https://oomake.com/download/docker-windows （百度网盘）
 https://mirrors.ustc.edu.cn/docker-ce/ （版本更新不及时）

下载后直接安装，安装时注意取消勾选window容器（默认不会勾选）。

Docker安装成功后，执行cmd命令`docker version`。

### 4.拉image出错

```sh
右键点击桌面顶栏的 docker 图标，选择 Preferences ，在 Daemon 标签（Docker 17.03 之前版本为 Advanced 标签）下的 Registry mirrors 列表中加入下面的镜像地址:
http://141e5461.m.daocloud.io
点击 Apply & Restart 按钮使设置生效。
```



