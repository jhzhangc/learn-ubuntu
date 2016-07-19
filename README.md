# learn-ubuntu
I am a start for linux

# Ubuntu学习笔记
## 常用安装日志
### 1. 双系统windows解决8小时时差的问题
最好用的就是这种方法
```
sudo timedatectl set-local-rtc 1
```
### 2. 禁用访客用户
可以不设置，访客模式无法查看正常用户的数据
```
echo allow-guest=false | sudo tee -a /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf
```
### 3. N显卡驱动
尝试过在官网下载，但是造成了系统重启后无法进入的问题，最佳解决方案还是在系统更新中选择相应的驱动。
### 4. 将unity移动到底部
在使用dock之后，unity除了win键，其它时候基本无用。
```
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```
### 5. 点击图标最小化
在别人的日志中学习来的，没有尝试过。
```
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshel
```
### 6. 删除libreoffice
WPS还是要比默认带的libreoffice更适合国人。
```
sudo apt-get remove libreoffice-common
```
### 7. 删除Amazon的链接
```
sudo apt-get remove unity-webapps-common
```
### 8. 删掉基本不用的自带软件（其它）
其它无用的一起列在这里了
```
sudo apt-get remove thunderbird totem rhythmbox empathy brasero simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-orca webbrowser-app gnome-sudoku  landscape-client-ui-install

sudo apt-get remove onboard deja-dup
```
### 9. 安装Vim
Vim神器不再多言，必须安装
```
sudo apt-get install vim
```
如果想使用markdown还是建议使用haroopad不建议直接在vim中安装插件。
如果是在windows系统中，安装vim后，有不能输入中文的问题，可用以下的方法解决：
```
set fileencodings=utf-8,ucs-bom,cp936,big5
set fileencoding=utf-8
```
默认主题的设置
`colorscheme desert`
windows下取消每次的~备份文件，加入设置如下：
`set nobackup`
### 10. 安装Google-Chrome
首先从官网下载最新的deb文件
然后进行安装
```
sudo apt-get install libappindicator1 libindicator7
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get -f install
```
在命令行中用 google-chrome 来打开浏览器
### 11. 安装五笔输入法
```
sudo apt-get install fcitx-table-wubi
```
### 12. 安装WPS Office
```
sudo apt-get install wps-office
```
### 13. 安装Oracle Java
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
由于系统自带的是OpenJDK，卸载OpenJDK之后会带有残留，导致运行
```java -version```
时第一行不是java的版本号，会是Picked up JAVA_TOOL_OPTIONS: -javaagent:/usr/share/java/jayatanaag.jar这个提示，导致很多检测java版本号的脚本会运行出错，因此需要手动清除残留。
```
sudo rm /usr/share/upstart/sessions/jayatana.conf
```
删除/usr/share/upstart/sessions/jayatana.conf文件
重启之后再运行java -version就不会再有
Picked up JAVA_TOOL_OPTIONS: -javaagent:/usr/share/java/jayatanaag.jar提示了
### 14. 安装Sublime Text 3
很优秀的编辑器，但是更建议用vim
```
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text
```
### 15. 翻墙lantern
```
sudo dpkg -i lantern.deb
```
如果启动有问题，可以继续用下面的方法
```
sudo chmod -R 777 /usr/bin/lantern
```
### 16. 主题优化
dock界面
```
sudo apt-add-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-icon-theme-circle //安装图标
sudo apt-get install numix-gtk-theme          //安装主题
```
透明度是用unity-tweak或者unity-tweak-tool调的
```
sudo apt-get install unity-tweak-tool
```
安装好之后就打开 Unity Tweak Tool 优化工具，在 GTK + 中选择使用 Numix 主题，并在 Icons 中选择使用 Numix-Circle 系列图标
安装 compizconfig-settings-manager 软件中心有，这个可以调整通知栏透明度，
然后就是安装docky：
```
sudo apt-get install docky
```
隐藏原来的任务栏：
> 先进“系统设置”>“外观”>"行为"
> 把“自动隐藏启动器”的“关闭”改成“开启”
> 下面的“呈现灵敏度”调到最左面，也就是最低 0
> 这样任务栏就再不会出来了
> 想改回去就把“自动隐藏”改回“关闭”状态

### 17. flash
如果使用的是CHROME则可以忽略。从官网下载的flash每次开机有报错，如果用firefox直接用了这个
```
sudo apt-get install browser-plugin-freshplayer-pepperflash
```
### 18. Cisco VPN
经验证，公司未开放linux系统下的VPN连接，无法连接
**安装过程**：
1. 下载anyconnect
	http://www.iqlinkus.net/download.action	
	http://www.iqlinkvpn.com/downloads/anyconnect-predeploy-linux-64-3.1.00495-k9.tar.gz
2. 解压source包，tarzxvf anyconnect-predeploy-linux-64-3.1.00495-k9.tar.gz
3. 进入安装文件目录cdanyconnect-3.1.00495/vpn
4. 安装sudo./vpn_install.sh
5. 查看安装情况ps aux  |  grep  cisco，显示如下即安装成功。
       root     3255  0.0  0.0 136124  6336 ?       Sl   08:59   0:05/opt/cisco/anyconnect/bin/vpnagentd
6. 在搜索您的电脑和在线资源中，输入vpn即可以找到软件，点击即可以打开界面。
**问题解决**：
输入ip之后点击链接报错：
UntrustedVPN Server Blocked!
AnyConnectcannot verify the VPN server: 221.183.16.27
Connectingto this server may result in a severe security compromise!
AnyConnectis configured to block untrusted VPN servers by default. Most userschoose to keep this setting.
Ifthis setting is changed, AnyConnect will no longer automaticallyblock connections to potentially malicious network devices.
进入设置界面，将最后一项勾选”Blockconnection to untrusted servers”去除掉，即可以解决问题。

### 19. Ubuntu Android Studio不能输入中文解决
```
export XMODIFIERS=@im=fcitx
export QT_IM_MODULE=fcitx
```
### 20. MarkDown编辑软件跨平台
http://pad.haroopress.com/user.html

### 21.WINE的安装和配置
#### 21.1.WINE的安装
- 在ubuntu软件中心搜索wine，选择"Wine Windows 程序加载器“安装（这种方法一般不是最新版本）
- http://www.winehq.org/download
- 终端分次输入下面的命令
```
sudo dpkg --add-architecture i386
sudo add-apt-repository ppa:wine/wine-builds
sudo apt-get update
sudo apt-get install --install-recommends winehq-devel
```

#### 21.2.WINE的配置
输入命令winecfg，或者dash里找到winetricks，出现wine的配置界面：
![](pic/wine_1.jpg)

- Windows版本，根据硬件情况而定
- 桌面：在显示项，第一个为全屏下捕捉鼠标，给全屏应用的；第二个，效果为让wine的程序窗口样子像xp，其实很难看；第三个，勾；第四个，通常没必要

#### 21.3.重要命令
- 其实可以直接点击exe程序运行，但如果遇到问题就不能诊断了；命令运行格式：
```
wine 程序名
```
注意：须先cd到程序所在文件。

- 注册表命令
```
wine regedit
```



