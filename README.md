# ubuntu-for-Android
 在Ubuntu搭建安卓开发环境
## 安装ubuntu
### 步骤
http://www.linuxdiyf.com/linux/20012.html
* 如果是Windows与Linux双系统安装，请选择其他选项，切记。您可以自己创建、调整分区，或者为 Ubuntu 选择多个分区。
* 四个分区即可/boot、/、/home、swap。/home尽量给大点，因为平时使用的主要目录还是这里,独立

### 优化
http://noogel.xyz/2017/06/17/1.html
* 更新前先设置源为aliyun的，国内访问速度快。
```
sudo apt-get update
sudo apt-get upgrade
```
* 删除Amazon的链接
```
sudo apt-get remove unity-webapps-common
```
* 卸载libreOffice(用WPS来替代)
```
sudo apt-get remove libreoffice-common
```
* 删除不常用的软件
```
sudo apt-get remove thunderbird totem rhythmbox empathy brasero simple-scan gnome-mahjon
sudo apt-get remove gnome-mines cheese transmission-common gnome-orca webbrowser-app gno
sudo apt-get remove onboard deja-dup
```

### 美化
* 先装 Unity 图形管理工具
```
sudo apt-get install unity-tweak-tool
```
* 安装 Flatabulous 主题
```
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme
```
* 安装配套图标
```
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
```
* 安装字体(文泉)
```
sudo apt-get install fonts-wqy-microhei
```
* 安装zsh(以及 oh-my-zsh)
```
sudo apt-get install zsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
chsh -s /usr/local/bin/zsh
```

### 必备软件
* vim
```
sudo apt-get install vim
```
* git
```
sudo apt-get install git
```
* 压缩软件RAR
```
sudo apt-get install rar
```
* curl <br/>
https://curl.haxx.se/download.html
```
sudo apt-get install curl
```
* jq <br/>
https://stedolan.github.io/jq/
```
sudo apt-get install jq
```
* Shadowsocks-Qt5 <br/>
https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
* chrome
https://www.google.com/chrome/browser/desktop/index.html
```
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
* SwitchyOmega
https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList

* shutter
```
sudo apt-get install shutter
```
* 搜狗输入法 <br/>
https://pinyin.sogou.com/linux/?r=pinyin

* wps <br/>
http://linux.wps.cn/
```
sudo dpkg -i wps-office_10.1.0.5672~a21_amd64.deb
sudo apt-get install -f
```
* gimp
```
sudo apt-get install gimp
```
* System Load Indicator（系统状态指示器）
```
sudo add-apt-repository ppa:indicator-multiload/stable-daily
sudo apt-get update
sudo apt-get install indicator-multiload
```
* Atom <br/>
https://atom.io/
```
sudo dpkg -i atom-amd64.deb
sudo apt-get -f install
```

### 驱动
* Qualcomm Atheros Device wifi驱动<br>
https://askubuntu.com/questions/708061/qualcomm-atheros-device-168c0042-rev-30-wi-fi-driver-installation

```
#查看驱动型号
lspci -vvnn | grep Network

sudo apt-get install build-essential linux-headers-$(uname -r) git
echo "options ath10k_core skip_otp=y" | sudo tee /etc/modprobe.d/ath10k_core.conf
wget https://www.kernel.org/pub/linux/kernel/projects/backports/stable/v4.4.2/backports-4.4.2-1.tar.gz
tar -zxvf backports-4.4.2-1.tar.gz
cd backport-4.4.2-1
make defconfig-wifi
make
sudo make install
git clone https://github.com/kvalo/ath10k-firmware.git
sudo cp -r ath10k-firmware/QCA9377 /lib/firmware/ath10k/
sudo cp /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin_WLAN.TF.1.0-00267-1 /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin
#需要重启才能生效

#如果更新了内核导致wifi驱动失败
cd backports-4.4.2-1
make clean
make defconfig-wifi
make
sudo make install

#查看wifi是否禁用
rfkill list
#开启wifi
rfkill unblock all
```
