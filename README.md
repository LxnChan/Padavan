![Pic Of Lxn-Padavan](https://github.com/LxnChan/Padavan/blob/main/pic/pic220321a.png?raw=true)

## Lxn-Padavan

想做最简洁、最轻快、最实用的Padavan固件。

### Padavan
- 基于hanwckf的Padavan仓库制作
- 使用[gorden5566](https://github.com/gorden5566/padavan)的汉化字典
- [curl](https://github.com/curl/curl)可选编译可执行程序 ```CONFIG_FIRMWARE_INCLUDE_CURL``` **添加了SSL完整支持。**
- 使用了[PROMETHEUS](http://pm.freize.net/index.html)提供的部分补丁
- 使用了[Linaro1985/padavan-ng](https://gitlab.com/padavan-ng/padavan-ng)的部分软件包
- 可选以下插件：
>- [scutclient](https://github.com/hanwckf/scutclient) ```CONFIG_FIRMWARE_INCLUDE_SCUTCLIENT```
>- [gdut-drcom](https://github.com/chenhaowen01/gdut-drcom) ```CONFIG_FIRMWARE_INCLUDE_GDUT_DRCOM```
>- [dogcom](https://github.com/hanwckf/dogcom) ```CONFIG_FIRMWARE_INCLUDE_DOGCOM```
>- [minieap](https://github.com/hanwckf/minieap) ```CONFIG_FIRMWARE_INCLUDE_MINIEAP```
>- [njit-client](https://github.com/hanwckf/njit8021xclient) ```CONFIG_FIRMWARE_INCLUDE_NJIT_CLIENT```
>- [napt66](https://github.com/mzweilin/napt66) ```CONFIG_FIRMWARE_INCLUDE_NAPT66```
>- [softether-vpnserver](https://github.com/SoftEtherVPN/SoftEtherVPN_Stable) ```CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_SERVER```
>- [softether-vpnclient](https://github.com/SoftEtherVPN/SoftEtherVPN_Stable) ```CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_CLIENT```
>- [softether-vpncmd](https://github.com/SoftEtherVPN/SoftEtherVPN_Stable) ```CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_CMD```
>- [vlmcsd](https://github.com/hanwckf/vlmcsd) ```CONFIG_FIRMWARE_INCLUDE_VLMCSD```
>- [ttyd](https://github.com/tsl0922/ttyd) ```CONFIG_FIRMWARE_INCLUDE_TTYD```
>- [lrzsz](https://ohse.de/uwe/software/lrzsz.html) ```CONFIG_FIRMWARE_INCLUDE_LRZSZ```
>- [htop](https://hisham.hm/htop/releases/) ```CONFIG_FIRMWARE_INCLUDE_HTOP```
>- [nano](https://www.nano-editor.org/dist/) ```CONFIG_FIRMWARE_INCLUDE_NANO```
>- [iperf3](https://github.com/esnet/iperf) ```CONFIG_FIRMWARE_INCLUDE_IPERF3```
>- [dump1090](https://github.com/hanwckf/dump1090) ```CONFIG_FIRMWARE_INCLUDE_DUMP1090```
>- [rtl-sdr](https://github.com/osmocom/rtl-sdr) ```CONFIG_FIRMWARE_INCLUDE_RTL_SDR```
>- [samba3.6](https://gitlab.com/padavan-ng/padavan-ng/tree/master/trunk/user/samba36) ```CONFIG_FIRMWARE_INCLUDE_SMBD36```
>- [mtr](https://github.com/traviscross/mtr) ```CONFIG_FIRMWARE_INCLUDE_MTR```
>- [socat](http://www.dest-unreach.org/socat) ```CONFIG_FIRMWARE_INCLUDE_SOCAT```
>- [srelay](https://socks-relay.sourceforge.io) ```CONFIG_FIRMWARE_INCLUDE_SRELAY```
>- [3proxy](https://github.com/z3APA3A/3proxy) ```CONFIG_FIRMWARE_INCLUDE_3PROXY```
>- [mentohust](https://github.com/hanwckf/mentohust-1) ```CONFIG_FIRMWARE_INCLUDE_MENTOHUST```
>- [frpc](https://github.com/fatedier/frp) ```CONFIG_FIRMWARE_INCLUDE_FRPC```
>- [frps](https://github.com/fatedier/frp) ```CONFIG_FIRMWARE_INCLUDE_FRPS```
>- [tunsafe](https://github.com/TunSafe/TunSafe) ```CONFIG_FIRMWARE_INCLUDE_TUNSAFE```
>- [wireguard-go](https://git.zx2c4.com/wireguard-go/) ```CONFIG_FIRMWARE_INCLUDE_WIREGUARD```
>- [smartdns](https://github.com/pymumu/smartdns) ```CONFIG_FIRMWARE_INCLUDE_SMARTDNS```

- 已适配除官方适配外的以下机型
>- MI-MINI (USB)
>- MI-R4A
>- MI-NANO
>- K2P
>- K2P-USB (USB)

### 编译

- 安装依赖包

```shell
# Ubuntu 20.04 LTS
sudo apt update
sudo apt install unzip libtool-bin curl cmake gperf gawk flex bison nano xxd \
	fakeroot kmod cpio git python3-docutils gettext automake autopoint \
	texinfo build-essential help2man pkg-config zlib1g-dev libgmp3-dev \
	libmpc-dev libmpfr-dev libncurses5-dev libltdl-dev wget libc-dev-bin
```

- 克隆源码

```shell
git clone --depth=1 git@github.com:LxnChan/Padavan.git /opt/rt-n56u
git clone --depth=1 git@bitbucket.org:lxnchan/main.git /opt/rt-n56u
```

- 准备工具链

```shell
cd /opt/rt-n56u/toolchain-mipsel

# （推荐）使用脚本下载预编译的工具链：
sh dl_toolchain.sh

# 或者，也可以从源码编译工具链，这需要一些时间：
./clean_toolchain
./build_toolchain
```

也可以在[这](https://github.com/LxnChan/Padavan/releases/tag/Toolchain) 下载，自己改一下dl_toolchain.sh脚本的下载地址就行。

- 修改机型配置文件

```shell
vim /opt/rt-n56u/trunk/configs/templates/MI-R4A.config
```

- 开始编译

```shell
cd /opt/rt-n56u/trunk
# 对于WSL环境，建议使用sudo进行编译，或者使用fakeroot-tcp代替fakeroot
fakeroot ./build_firmware_modify MI-R4A
# 脚本第一个参数为路由型号，在trunk/configs/templates/中
# 编译好的固件在trunk/images里
# 首次编译完成后，如果需要再次编译其它固件，需要执行清理脚本：
./clear_tree
```

