# 虚拟机ROS环境配置

- [环境介绍](#环境介绍)
- [安装Ubuntu 16](#安装ubuntu-16)
- [ROS安装](#ros安装)
- [其他软件安装](#其他软件安装)

## 环境介绍

与硬件相关的许多开发环境在Windows下比较方便, 同时, ROS在Ubuntu下使用比较方便, 为了联调时不用背两个电脑, 可以在Win10环境下使用虚拟机(Virtual Box或者VMware Workstation)安装Ubuntu 16, 然后配置ROS开发环境, 网络的设置需要注意一下.  

我的笔记本配置: i7-8550U, 16G, 512G SSD, Win10 下虚拟机安装Ubuntu 16运行流畅.  

## 安装Ubuntu 16

- Win10安装虚拟机(略)
- 下载 [Ubuntu 16.04.5 LTS (Xenial Xerus) - 64-bit PC (AMD64) desktop image](http://releases.ubuntu.com/16.04/)
- 虚拟机里选择下载的.iso文件安装, 内存4GB, 处理器2*2, 硬盘60GB, **网络适配器选择桥接模式(B): 直接连接物理网络**.
- 接下来一步步安装就可以了.  
- 可能需要在BIOS中使能 Intel VT-x

## ROS安装

- 网速好的话(5MB/s左右)大概10分钟可以完成本节操作
- 更换软件源: System Settings -> Software & Updates -> Ubuntu Software选项卡 -> Download from: http://mirrors.tuna.tsinghua.edu.cn/ubuntu, 改成清华的源, 点击Close后点击Reload.
- 打开 [在Ubuntu中安装ROS Kinetic](http://wiki.ros.org/cn/kinetic/Installation/Ubuntu) 网页.
- 1.2中点击Mirros, 复制 1.1.3 Tsinghua University的Command 到终端:  

    ```s
    sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
- 返回 [在Ubuntu中安装ROS Kinetic](http://wiki.ros.org/cn/kinetic/Installation/Ubuntu) 网页, 复制1.3 添加keys到终端:  

    ```s
    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
    ```
- 更新:  

    ```s
    sudo apt-get update
    ```

- 桌面完整版安装:  

    ```s
    sudo apt-get install ros-kinetic-desktop-full
    ```

- 初始化rosdep:

    ```s
    sudo rosdep init
    rosdep update   # 一次不行多来几遍, 最好能访问外网
    ```

- 环境配置:  

    ```s
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```

- 构建工厂依赖:  

    ```s
    sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
    ```

## 其他软件安装

### VS Code

### Gitkraken

### 搜狗输入法

- 参考 [ubuntu16.04下成功安装搜狗输入法](https://blog.csdn.net/woainishifu/article/details/71420303)

- 安装 fcitx 及其相关工具:  

    ```s
    sudo apt-get install fcitx
    sudo apt-get install fcitx-config-gtk
    sudo apt-get install fcitx-table-all
    sudo apt-get install im-switch
    ```

- 下载安装 [搜狗输入法for Linux 64bit](https://pinyin.sogou.com/linux/?r=pinyin)
- 重启或者log out -> log in
- 找到 Fcitx Configuration -> 左下角+ -> 去掉 Only Show Current Language 的勾选 -> 下拉找到 Sogou Pinyin -> OK
- Ctrl + Space切换输入法, Shift切换中英文, Shift + Space切换全半角, Ctrl + .切换中英文标点
