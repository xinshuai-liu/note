1 设置清华源
sudo sed -i "s/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list
sudo sed -i "s/cn.mirrors.tuna/mirrors.tuna/g" /etc/apt/sources.list
sudo apt-get update

2 安装必要工具
apt-get install build-essential    # build-essential packages, include binary utilities, gcc, make, and so on
apt-get install man                # on-line reference manual
apt-get install gcc-doc            # on-line reference manual for gcc
apt-get install gdb                # GNU debugger
apt-get install git                # revision control system
apt-get install libreadline-dev    # a library used later
apt-get install libsdl2-dev        # a library used later
apt-get install vim
apt-get install cmake

3 设置root密码
sudo passwd

4 去除vscode白色标题栏
设置 << 用户 << 窗口 << Title Bar Style << 更改选项为 “custom”

修改计算机名称
sudo vim /etc/hosts
vim /etc/hostname

更新snap 先关闭再更新
sudo snap refresh snap-store