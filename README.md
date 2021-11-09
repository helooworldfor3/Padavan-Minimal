# Padavan精简版固件，适合不爱折腾固件的用户
固件默认wifi名称PDCN及PDCN_5G  
wifi密码1234567890  
管理地址192.168.123.1  
管理账号密码都是admin 
***

- 20211109更新
>- 精简插件，仅保留路由器常用功能  
（只精简了NEWIFI3的固件，其它版本固件请参考/trunk/configs/NEWIFI3.config中的插件选项）
>- 优化科学上网插件中的DNS选项，加入对SmartDNS的支持
>- 移除VPN界面选项
>- 修复部分系统编译skipdbv2插件报错的问题

NEWIFI3固件下载  
https://www.lanzouw.com/iOn6Vwcaati
***

# Padavan-Minimal
在原作者keke1023整合的固件版本上做了精简和DNS优化  
https://github.com/keke1023/Padavan  

推荐使用云编译脚本进行固件编译  
https://github.com/pmkol/Padavan-build

# Padavan
基于hanwckf,chongshengB以及padavanonly的源码整合而来，支持kvr  
编译方法同其他Padavan源码，主要特点如下：  
1.采用padavanonly源码的5.0.4.0无线驱动，支持kvr  
2.添加了chongshengB源码的所有插件  
3.其他部分等同于hanwckf的源码，有少量优化来自immortalwrt的padavan源码  
4.添加了MSG1500的7615版本config  
  
以下附上他们四位的源码地址供参考  
https://github.com/hanwckf/rt-n56u  
https://github.com/chongshengB/rt-n56u  
https://github.com/padavanonly/rt-n56u  
https://github.com/immortalwrt/padavan  

- 已适配除官方适配外的以下机型
>- PSG1208
>- PSG1218
>- 5K-W20 (USB)
>- OYE-001 (USB)
>- NEWIFI-MINI (USB)
>- MI-MINI (USB)
>- MI-3 (USB)
>- MI-3C
>- MI-4
>- MI-R3G (USB)
>- MI-R4A
>- MI-R3P (USB)
>- HC5661A
>- HC5761A (USB)
>- HC5861B
>- 360P2 (USB)
>- MI-NANO
>- MZ-R13
>- MZ-R13P
>- RT-AC1200GU (USB)
>- XY-C1 (USB)
>- WR1200JS (USB)
>- NEWIFI3 (USB)
>- B70 (USB)
>- A3004NS (USB)
>- K2P
>- K2P-USB (USB)
>- JCG-836PRO (USB)
>- JCG-AC860M (USB)
>- DIR-882 (USB)
>- DIR-878
>- MR2600 (USB)
>- WDR7300
>- RM2100
>- CR660x (CR6606, CR6608, CR6609)
>- R2100
>- JCG-Y2 (USB)
>- E8820V2 (USB)
>- ZTE_E8820S (USB)
>- MSG1500 (USB)
>- R6220 (USB)
>- NETGEAR-CHJ (R6260, R6350, R6850, WAC124)
>- NETGEAR-BZV (R6800, R6700-v2, R7200, Nighthawk AC2400)

***

# 编译说明

* 安装依赖包

```shell
# Debian/Ubuntu
sudo apt update
sudo apt install unzip libtool-bin curl cmake gperf gawk flex bison nano xxd \
	fakeroot kmod cpio git python-docutils gettext automake autopoint \
	texinfo build-essential help2man pkg-config zlib1g-dev libgmp3-dev \
	libmpc-dev libmpfr-dev libncurses5-dev libltdl-dev wget libc-dev-bin

# Archlinux/Manjaro
sudo pacman -Syu --needed git base-devel cmake gperf ncurses libmpc \
        gmp python-docutils vim rpcsvc-proto fakeroot cpio help2man

# Alpine
sudo apk add make gcc g++ cpio curl wget nano xxd kmod \
	pkgconfig rpcgen fakeroot ncurses bash patch \
	bsd-compat-headers python2 python3 zlib-dev \
	automake gettext gettext-dev autoconf bison \
	flex coreutils cmake git libtool gawk sudo

# CentOS 7
sudo yum update
sudo yum groupinstall "Development Tools"
sudo yum install ncurses-* flex byacc bison zlib-* texinfo gmp-* mpfr-* gettext \
	libtool* libmpc-* gettext-* python-docutils nano help2man fakeroot

# CentOS 8
sudo yum update
sudo yum groupinstall "Development Tools"
sudo yum install ncurses-* flex byacc bison zlib-* gmp-* mpfr-* gettext \
	libtool* libmpc-* gettext-* nano fakeroot

# CentOS 8不能直接通过yum安装texinfo，help2man，python-docutils。请去官网下载发行的安装包编译安装
# 以texinfo为例
# cd /usr/local/src
# sudo wget http://ftp.gnu.org/gnu/texinfo/texinfo-6.7.tar.gz
# sudo tar zxvf texinfo-6.7.tar.gz
# cd texinfo-6.7
# sudo ./configure
# sudo make
# sudo make install

```

* 克隆源码

```shell
git clone --depth=1 https://github.com/pmkol/Padavan-Minimal.git /opt/rt-n56u
```

* 准备工具链

```shell
cd /opt/rt-n56u/toolchain-mipsel

# （推荐）使用脚本下载预编译的工具链：
sh dl_toolchain.sh

# 或者，也可以从源码编译工具链，这需要一些时间：
./clean_toolchain
./build_toolchain

```

* (可选) 修改机型配置文件

```shell
nano /opt/rt-n56u/trunk/configs/templates/NEWIFI3.config
```

* 清理代码树并开始编译

```shell
cd /opt/rt-n56u/trunk
./clear_tree
fakeroot ./build_firmware_modify NEWIFI3
# 脚本第一个参数为路由型号，在trunk/configs/templates/中
# 编译好的固件在trunk/images里
```

***

### 请参阅 ###
- https://www.jianshu.com/p/c31b58728778
- https://www.jianshu.com/p/6b8403cdea46
