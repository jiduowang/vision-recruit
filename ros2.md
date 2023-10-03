# 引言
机器人的发展横跨七八十年，经历了三个重要时期。


2000年前，机器人主要应用于工业生产，俗称工业机器人，由示教器操控，帮助工厂释放劳动力，此时的机器人并没有太多智能而言，完全按照人类的命令执行动作，更加关注电气层面的驱动器、伺服电机、减速机、控制器等设备，这是机器人的电气时代。

2000年后，计算机和视觉技术逐渐应用，机器人的类型不断丰富，出现了AGV、视觉检测等应用，此时的机器人传感器更加丰富，但是依然缺少自主思考的过程，智能化有限，只能感知局部环境，这是机器人的数字时代，不过这也是机器人大时代的前夜。

2015年之后，随着人工智能技术的快速发展，机器人成为了AI技术的最佳载体，家庭服务机器人、送餐机器人、四足仿生机器狗、自动驾驶汽车等应用呈井喷状爆发，智能机器人时代正式拉开序幕。

智能机器人的快速发展，必将对机器人开发提出更高的要求，软件层面最为热点的技术之一就是机器人操作系统，这也是我们课程的主角——Robot Operating System（即ROS）。

---
# ROS2安装方法

目前来讲，Linux发展迅猛，已经成为了性能稳定的多用户操作系统，也是ROS2依赖的重要底层系统。虽然ROS2目前也支持Windows、MacOS，但对Linux系统的支持最好，在本教程中，我们主要讲解Linux之上的ROS2使用方法，其他系统原理也基本相同。

本教程将使用Ubuntu22.04LTS版本来作为我们的操作系统，安装方法很多，如果你之前已经熟悉Linux，建议在电脑上硬盘安装Ubuntu，这样可以发挥出硬件最大的性能，如果你是第一次接触Linux，建议在已有的windows上通过虚拟机安装，未来熟悉之后再考虑硬盘安装。（个人建议还是利用虚拟机进行调试，双系统崩溃之后可能会影响到主系统，同时出现问题重新安装比较麻烦）

系统镜像：<https://ubuntu.com/download/desktop>

VMware16Pro： <https://www.aliyundrive.com/s/SaE6abZYjAP>

16pro密钥：<https://www.haozhuangji.com/xtjc/145413111.html>

VMware17：<https://www.aliyundrive.com/s/quVKXGzbBzJ>


具体安装可自行到CSDN查看
推荐安装配置：硬盘30G，内存4G，处理器数量2， 每个处理器的核心数4， 请视个人电脑情况安装，后续可以调整

## 接下来，我们就可以把ROS2安装到Ubuntu系统中了。安装步骤如下：

### 1.设置编码


	$ sudo apt update && sudo apt install locales
	$ sudo locale-gen en_US en_US.UTF-8
	$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 
	$ export LANG=en_US.UTF-8


### 2.添加源
	$ sudo apt update && sudo apt install curl gnupg lsb-release 
	$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg 
	$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

如遇报错“Failed to connect to raw.githubusercontent.com”，可参https://www.guyuehome.com/37844

### 3.安装ROS2
	$ sudo apt update
	$ sudo apt upgrade
	$ sudo apt install ros-humble-desktop

### 4.设置环境变量
	$ source /opt/ros/humble/setup.bash
	$ echo " source /opt/ros/humble/setup.bash" >> ~/.bashrc 

---
# ROS2开发环境配置
### Git
git是一个版本管理软件，也是因Linux而生。
	$ sudo apt install git

### VScode
下载链接：<https://code.visualstudio.com/Download>  

插件配置：中文语言包、python插件、c++插件、CMake、vscode-icons、ROS、Msg Language Support、 Visual Studio IntelliCode、URDF、Markdown All in One

---
# 工作空间
### 创建工作空间：
	$ mkdir -p ~/dev_ws/src	
	$ cd ~/dev_ws/src

### 自动安装依赖：
	$ sudo apt install -y python3-pip
	$ sudo pip3 install rosdepc
	$ sudo rosdepc init
	$ rosdepc update
	$ cd ..
	$ rosdepc install -i --from-path src --rosdistro humble -y

### 编译工作空间：
	$ sudo apt install python3-colcon-ros
	$ cd ~/dev_ws/
	$ colcon build

### 设置环境变量：
	$ source install/local_setup.sh # 仅在当前终端生效
	$ echo " source ~/dev_ws/install/local_setup.sh" >> ~/.bashrc # 所有终端均生效

