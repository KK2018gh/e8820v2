添加了E8820V2的支持，优先使用了闭源驱动（开机不启动WIFI需要到后台手动开启）

更新了大功率EEPROM但是效果有点不尽人意，可以直接在breed中升级，然后修改MAC地址即可

精简了一下内核，默认7621全系列超频至1.1Ghz

添加了OpenClah，istore
## 2023/6/2
添加了ASUS AC1200GU的支持
添加了龙尚8300w的id支持

## 注意

1. **不要用 root 用户进行编译**
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1 密码 password

## 编译命令

1. 首先装好 Linux 系统，推荐 Debian 11 或 Ubuntu LTS

2. 安装编译依赖

   ```bash
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 aria2 asciidoc autoconf automake autopoint binutils bison build-essential \
   bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
   git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
   libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
   mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pip libpython3-dev qemu-utils \
   rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
   ```

3. 下载源代码，更新 feeds 并选择配置

   ```bash
   git clone https://github.com/MoShengQ7/lede.git
   cd lede
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```

4. 下载 dl 库，编译固件
（-j 后面是线程数，第一次编译推荐用单线程）

   ```bash
   make download -j8
   make V=s
   ```
附加：添加主题:
   ```bash
   cd lede
   rm -rf  package/lean/luci-theme-argon
   git clone -b 18.06 https://github.com/jerrykuku/luci-theme-argon.git package/lean/luci-theme-argon
   git clone https://github.com/jerrykuku/luci-app-argon-config.git package/lean/luci-app-argon-config
   git clone -b openwrt-18.06 https://github.com/rosywrt/luci-theme-rosy.git package/lean/luci-theme-rosy
   git clone -b 18.06 https://github.com/kiddin9/luci-theme-edge.git package/lean/luci-theme-edge
   ```
如果需要重新配置：
   ```bash
   rm -rf ./tmp && rm -rf .config
   ```
如果需要清理缓存：
   ```bash
   make clean
   ```
