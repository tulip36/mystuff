manjaro 安装后配置
 2019-05-12 |  Manjaro ， beautify
 3.1k |  15
 评论次数 0 |  阅读次数 427
小白配置 Manjaro 的辛酸历史，自己虽然linux学的不是很高深，但奈何搞坏系统的能力与日俱增，配置 Manjaro 环境也有7~8次了，配置过 xfce桌面、gnome桌面、kde桌面，这里主要是 Manjaro + kde.
同步远程数据包到本地
没有同步数据包的话，安装软件时可能会出现数据包找不到的 warning，终端执行

sudo pacman -Syy
安装 vim
vim 无疑是linux下最好用的编辑器，不是很熟悉vim 的可以终端执行

vimtutor
获取 《VIM 教程》，讲述了一些必要的基本命令，效果还可以，接下来假定你已经会使用 vim编辑器，如果实在不想学习vim，可以使用一些其他的编辑器，如 nano，也是很方便

安装 vim

sudo pacman -S vim
添加 archlinuxCN 源
编辑 pacman.conf 配置文件

sudo vim /etc/pacman.conf
在底部添加(连续按’GG’就可以跳转到文章尾)：

[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
然后终端执行，更新数据包

sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
更新
sudo pacman -Syu
这一下更新包较多，大概1.5G

MacBook Air 安装 Manjaro 不能连接无线网
Mac 使用的是博通的网卡，需要自己安装无限网卡驱动，可以使用 “inxi -F” 查看自己的网卡型号

Network:
  Device-1: Broadcom and subsidiaries BCM4360 802.11ac Wireless Network Adapter
  driver: wl
  IF: wlp3s0 state: up mac: d0:81:7a:be:dd:80
我的网卡型号时 BCM4360

先连接有线网，sudo pacman -Syu 更新系统，然后在系统设置里找到内核，查看内核版本，选择与内核版本匹配的linux-headers，如我正在运行的内核是 Linux 4.19.36-1，选择 linux419-headers安装

sudo pacman -S linux-headers 或者 yaourt linux-headers
最后安装无线网卡驱动

sudo pacman -S broadcom-wl-dkms
重启，ok

安装搜狗输入法
Manjaro 下有很多可以选择的输入法，如搜狗、谷歌，个人感觉搜狗更加贴切国内用户的使用

sudo pacman -S fcitx-sogoupinyin
sudo pacman -S fcitx-im				# 全部安装
sudo pacman -S fcitx-configtool		# 图形化配置工具
然后配置中文输入发环境变量，编辑 ~/.xprofile文件（如果不存在，则新建），添加：

export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
重启后就可以正常使用了

安装常用软件
安装 yaourt & yay
sudo pacman -S yaourt yay
安装 git
sudo pacman -S git
设置个人 github 信息
git config --global user.name "github用户名"
git config --global user.email "注册邮箱"
安装 zsh – shell中的极品
安装 zsh (需要先把 git 安装好)

sudo pacman -S zsh
配置 oh-my-zsh

sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
更换默认的shell

chsh -s /bin/zsha
安装 chromium
chromium 是开发者版的谷歌浏览器，更新较为频繁

sudo pacman -S chromium
安装网易云音乐
桌面版：

sudo pacman -S netease-cloud-music
终端版：musicbox

yaourt musicbox
安装完后终端键入 musicbox 就可以体验终端版的网易云了

安装 WPS
sudo pacman -S wps-office
sudo pacman -S ttf-wps-fonts    # 安装wps字体
安装微信
sudo pacman -S electronic-wechat
安装 ssr
sudo pacman -S shadowsocks-qt5
安装坚果云
sudo pacman -S nutstore
安装 VScode
sudo pacman -S visual-studio-code-bin
安装主题
Warning: kde桌面

sudo pacman -S papirus-icon-theme
sudo pacman -S arc-kde kvantum-theme-arc
安装完成之后可以到设置里更改使用

安装 uget
sudo pacman -S uget aria2
chrome 启用 uget 下载
打开 uGet 选择 编辑 -> 设置 -> 插件，然后把插件匹配顺序改为：aria2

然后安装 chrome 浏览器插件

sudo pacman -S uget-intedrator
sudo pacman -S uget-intedrator-chrome
安装 pycharm professional
sudo pacman -S pycharm-professional
破解
。。。后续

安装 typora
sudo pacman -S typora
安装 PS 替代品 —— gimp
sudo pacman -S gimp
安装 flash
sudo pacman -S pepper-flash
sudo pacman -S flashplugin
配置：后续。。。

安装 mysql

安装 mysql
sudo pacman -S mysql
初始化
sudo mysqld --initialize --user=mysql --basedir=/usr --datedir=/var/lib/mysql
执行结束后默认创建一个 SQL 用户：root 以及 root用户密码

开机自启
sudo systemctl enable mysqld.service
启动 MySQL 服务
sudo systemctl start mysqld.service		# 启动
sudo systemctl status mysqld.service 	# 查看状态
连接数据库
mysql -uroot -p
输入刚才生成的 root 密码

修改 root 密码
首先要连接数据库，然后根据 mysql 版本键入命令

mysql 8

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
mysql 8.0 以下

ALTER user 'root'@'localhost' IDENTIFIED BY '新密码';
后续
mysql 身份验证问题，mariaDB的替换

安装 mycli
由于 mysql 在使用过程不提示命令，mycli就可以很好地解决这一点

sudo pacman -S mycli
但在MySQL 下，mycli 插件无法使用了，首先要确保 PyMySQL >= 0.6.7

pip install pymysql
安装 mysql workbench
数据库可视化也是很人性化的

sudo pacman -S mysql-workbench
Manjaro 下 mysql 巨坑
Manjaro 每次更新的时候，mysql 都有可能崩溃，因为更新的时候说不定哪个库或者依赖更新，而mysql没有及时更新都会造成 mysql 无法启动成功，很是头疼，正在考虑其他数据库 /(ㄒoㄒ)/~~

安装 gpick 取色工具
sudo pacman -S gpick
安装 redshift-gtk 护眼神器
sudo pacman -S redshift  # 或者 sudo pacman -S redshift-gtk
在系统设置设置自动启动就可以每次开机连接网络后自动开启护眼模式了

安装 pip
Manjaro 默认是有 pip的

sudo pacman -S wget
wget https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
安装 virtualbox
坑太多，后续。。。

更新后解决搜狗输入法乱码
sogou-qimpanel
提示找不到依赖库，重新建立软链接

sudo ln -s /usr/lib64/libidn.so.12.6.0 /usr/lib64/libidn.so.11
pacman 常用命令
pacman -S  	# 安装
pacman -R   # 删除
pacman -Rs  # 移除已安装不需要软件包
pacman -Rsc # 删除一个包，所有依赖
pacman -Syu # 升级包
pacman -Ss  # 查询包数据库
pacman -Qs  # 搜索已安装的包
pacman -Si  # 显示包大量信息
pacman -Qi  # 本地安装包
pacman -Sc  # 清理包缓存
Manjaro 搭建 Apache、Mysql、PHP 环境
安装 Apache
sudo pacman -S apache
查看 Apache 状态和版本信息

sudo systemctl status httpd
apachectl -v   	# 或者 httpd -v
设置开机启动

sudo systemctl enable httpd
sudo systemctl restart httpd
站点根目录

cd /srv/http/
安装 Mysql
a跳转

md跳转

安装 PHP
sudo pacman -S php php-apache
修改 apache 配置

sudo vim /etc/httpd/conf/httpd.conf
注释掉

LoadModule mpm_event_module modules/mod_mpm_event.so
去掉注释

LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
在末尾添加

LoadModule php7_module modules/libphp7.so
AddHandler php7-script php
Include conf/extra/php7_module.conf
测试 php

sudo vim /srv/http/test.php
键入php代码

<?php
    phpinfo();
?>
重启 apache

sudo systemctl restart httpd
浏览器访问 http://localhost/test.php

安装 phpMyAdmin
与 mysql workbench 类似，phpMyAdmin也是将数据库图形化，优点是浏览器访问，可以跨平台使用，也可以用在服务器端的数据库

sudo pacman -S phpmyadmin
编辑 php 配置文件

sudo vim /etc/php/php.ini
确认接下来几行没有被注释掉

[...]
extension=bz2.so		# 我的是 extension=bz2
extension=mysqli.so     # extension=mysqli
[...]
然后，创建 phpmyadmin的配置文件

sudo vim /etc/httpd/conf/extra/phpmyadmin.conf
添加：

Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
<Directory "/usr/share/webapps/phpMyAdmin">
DirectoryIndex index.php
AllowOverride All
Options FollowSymlinks
Require all granted
</Directory>
然后，打开 apache 配置文件

sudo vim /etc/httpd/conf/httpd.conf
末尾添加：

Include conf/extra/phpmyadmin.conf
重启 apache

sudo systemctl restart httpd
测试 phpmyadmin http://localhost/phpmyadmin

进入主界面如果在底部出现error: “The configuration file now needs a secret passphrase (blowfish_secret)” ，编辑

sudo vim /etc/webapps/phpmyadmin/config.inc.php
找到以下代码并编辑

$cfg['blowfish_secret'] = '`MyP@$S`'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH!$ /**
重启 apache

sudo systemctl restart httpd
坑，后续。。。

Manjaro 使用 Wine
安装配置 Wine
sudo pacman -S wine wine_gecko wine_mono
配置 64 & 32 位环境

mv ~/.wine ~/.wine64
# 使用WINEARCH建立32位环境配置
WINEARCH=win32 WINEPREFIX=~/.wine winecfg
安装32位显卡驱动

sudo pacman -S lib32-mesa lib32-nvidia-utils
设置字体
https://blog.csdn.net/zbgjhy88/article/details/85110956

后续。。。

运行 Windows 应用
wine exe文件名
安装 Windows 应用
msiexec -i msi安装包
卸载应用
wine uninstaller
wine 菜单管理
wine 中安装的应用可以在系统菜单中以 Wine 子菜单的形式呈现

后续。。。

Deepin-Wine
Deepin-Wine 是国产操作系统 Deepin 移植的Wine，对国内软件，有着更好的兼容性和使用体验

Warning: Deepin-Wine 32位

sudo pacman -S deepin-wine
安装 exe程序

deepin-wine QQBrowser.exe
打开注册表

deepin-wine regedit
bash 脚本
自己根据自己环境配置编写的 shell 文件，能够比较快捷简单的配置环境 manjaro.sh

#!/bin/bash
# manjaro 安装后配置以及软件安装

# 同步远程数据库到本地
sudo pacman -Syy

# 安装 vim
sudo pacman -S vim

# 添加 archlinuxCN 源
sudo echo "
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/\$arch" >> /etc/pacman.conf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring

# 更新
sudo pacman -Syu

# MacBook Air 安装无线网卡驱动
read -p "If your computer can connect to the wireless network(Y/N): " CONN
case "$CONN" in
    [yY] | [yY][eE][sS])
        echo "Ok, you are lucky :)"
        ;;
    [nN] | [nN][oO])
        echo "Sad, there are another packets you need to install :("

        read -p "If your system kernel is 4.19 and your network card model is Broadcom 4360(Y/N): " KERNEL
        case "$KERNEL" in
            [yY] | [yY][eE][sS])
                echo "Good Luck :)"
                sudo pacman -S linux419-headers broadcom-wl-dkms
                echo "Everything will be ok after reboot ..."

                read -p "If you want to reboot to use wireless network now(Y/N): " WIRELESS
                case "$WIRELESS" in
                    [yY] | [yY][eE][sS])
                        echo "reboot ..."
                        reboot
                        ;;
                    [nN] | [nN][oO])
                        echo "That's Ok, but you cannot use wireless network until reboot"
                        ;;
                    *)
                        echo "Invalid answer :/"
                        ;;
                esac
                
                reboot
                ;;
            [nN] | [nN][oO])
                echo "Sad, now I cannot resolve it ...."
                echo "But I will resolve soon"
                ;;
            *)
                echo "Invalid answer :/"
                ;;
        esac

        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac


#  安装搜狗输入法
sudo pacman -S fcitx-sogoupinyin fcitx-im fcitx-configtool
sudo echo "
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=\"@im=fcitx\"" >> ~/.xprofile
read -p "If you want to reboot to use sogoupinyin now(Y/N): " CHOOSE
case "$CHOOSE" in
    [yY] | [yY][eE][sS])
        echo "reboot ..."
        reboot
        ;;
    [nN] | [nN][oO])
        echo "Ok, but you cannot use sogoupinyin until reboot"
        ;;
    *)
        echo "Invalid choose :/"
        ;;
esac


# 安装常用的软件
sudo pacman -S yaourt yay git zsh chromium netease-cloud-music wps-office ttf-wps-fonts electronic-wechat shadowsocks-qt5 nutstore uget aria2 pepper-flash flashplugin redshift

# 安装软件配置编程环境
read -p "If you want to configure programming environment(Y/N): " CODE
case "$CODE" in
    [yY] | [yY][eE][sS])
        echo "You must be a qualified programmer :)"
        sudo pacman -S visual-studio-code-bin pycharm-professional typora gimp gpick 
        ;;
    [nN] | [nN][oO])
        echo "Your work must be more comfortable than me :("
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac

# 设置 github 信息
read -p "If you want to set your github info now(Y/N): " GITHUB
case "$GITHUB" in
    [yY] | [yY][eE][sS])
        read -p "Enter your github username: " GITHUB_USERNAME
        read -p "Enter your github registered email: " GITHUB_EMAIL
        git config --global user.name "$GITHUB_USERNAME"
        git config --global user.email "$GITHUB_EMAIL"
        echo "success to your github info"
        ;;
    [nN] | [nN][oO])
        echo "Ok, you can set it yourself later"
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac

# 配置 zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
chsh -s /bin/zsha

# 安装 musicbox
read -p "If you want to try musicbox(netease-cloud-music on terminal)(Y/N): " MUSICBOX
case "$MUSICBOX" in
    [yY] | [yY][eE][sS])
        yaourt musicbox
        echo "input \"musicbox\" in terminal, then you can have a try"
        ;;
    [nN] | [nN][oO]
        echo "Unfortunately, you miss a chance to \"装B\""
        ;;
    *)
        echo "Invalid choose :/"
        ;;
esac

# 安装主题
read -p "If your stystem is kde desktop(Y/N): " DESKTOP
case "$DESKTOP" in
    [yY] | [yY][eE][sS])

        read -p "Would you like to try another theme of your system(Y/N): " THEME
        case "$THEME" in
            [yY] | [yY][eE][sS])
                sudo pacman -S papirus-icon-theme arc-kde kvantum-theme-arc
                echo "success to theme"
                echo "You can choose the theme in system settings"
                ;;
            [nN] | [nN])
                echo "That's OK"
                ;;
            *)
                echo "Invalid answer :/"
                ;;
        esac

        ;;
    [nN] | [nN][oO])
        echo "That's OK"
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac


# 安装 mariadb
read -p "If you want to install mysql(mariadb is better in Manjaro)(Y/N): " MARIADB
case "$MARIADB" in
    [yY] | [yY][eE][sS])
        sudo pacman -S mariadb mycli mysql-workbench
        sudo mysqld --initialize --user=mysql --basedir=/usr --datedir=/var/lib/mysql
        
        read -p "If you want to start mysql when boot up: " MYSQL_START
        case "$MYSQL_START" in
            [yY] | [yY][eE][sS])
                sudo systemctl enable mysqld.service
                ;;
        esac

        sudo systemctl start mysqld.service
        echo "success to install mysql"
        echo "change mysql password by this: "
        echo "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码'; "
        ;;
    [nN] | [nN][oO])
        echo "That's Ok"
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac


# 搭建 Apache、PHP 环境
read -p "If you want to configure the environment with Apache and PHP(Y/N): " AP
case "$AP" in
    [yY] | [yY][eE][sS])
        sudo pacman -S apache phpmyadmin
        read -p "If you want to start Apache when boot up: " APACHE_START
        case "$APACHE_START" in
            [yY] | [yY][eE][sS])
                sudo systemctl enable httpd
                ;;
        esac
        sudo systemctl restart httpd
        echo "success to apache, and the location of site is /srv/http/"
        
        sudo pacman -S php php-apache
        echo "修改/etc/httpd/conf/httpd.conf 文件"

        sudo pacman -S phpmyadmin
        echo "编辑/etc/php/php.ini 文件"
        echo "
            Alias /phpmyadmin \"/usr/share/webapps/phpMyAdmin\"
            <Directory \"/usr/share/webapps/phpMyAdmin\">
            DirectoryIndex index.php
            AllowOverride All
            Options FollowSymlinks
            Require all granted
            </Directory>" >> /etc/httpd/conf/extra/phpmyadmin.conf
        echo "
            Include conf/extra/phpmyadmin.conf" >> /etc/httpd/conf/httpd.conf
        sudo systemctl restart httpd
        echo "访问 http://localhost/phpmyadmin"
        ;;
    [nN] | [nN][oO])
        "That's OK, you can configure youself later if you want"
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac


# 使用 Wine
read -p "If you want to use wine to run windows software(Y/N): " WINE
case "$WINE" in
    [yY] | [yY][eE][sS])
        sudo pacman -S wine wine_gecko wine_mono
        mv ~/.wine ~/.wine64
        WINEARCH=win32 WINEPREFIX=~/.wine winecfg
        sudo pacman -S lib32-mesa lib32-nvidia-utils

        read -p "If you want to use Deepin-Wine(Y/N): " DEEPIN_WINE
        case "$DEEPIN_WINE" in
            [yY] | [yY][eE][sS])
                sudo pacman -S deepin-wine
                ;;
        esac

        ;;
    [nN] | [nN][oO])
        echo "That's Ok"
        ;;
    *)
        echo "Invalid answer :/"
        ;;
esac


# 实现简单的图形界面
# 实现安装过的跳过
# 实现自动读取系统信息，配置个性化环境
# 如何获取最小权限修改只读文件


# 前序工作：
# chmod 755 manjaro.sh
# sudo ./manjaro.sh
