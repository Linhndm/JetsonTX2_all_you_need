# Ubuntu install of ROS Melodic

## Step1: Configure your Ubuntu repositories
Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse." You can follow the [Ubuntu guide](https://help.ubuntu.com/community/Repositories/Ubuntu) for instructions on doing this.
## Step2: Setup your sources.list
Setup your computer to accept software from packages.ros.org.
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
## Step3: Set up your keys
```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
If you experience issues connecting to the keyserver, you can try substituting hkp://pgp.mit.edu:80 or hkp://keyserver.ubuntu.com:80 in the previous command.

Alternatively, you can use curl instead of the apt-key command, which can be helpful if you are behind a proxy server:
```
curl -sSL 'http://keyserver.ubuntu.com/pks/lookup?op=get&search=0xC1CF6E31E6BADE8868B172B4F42ED6FBAB17C654' | sudo apt-key add -
```
## Step4: Installation
First, make sure your Debian package index is up-to-date:
```
sudo apt update
```
There are many different libraries and tools in ROS. We provided four default configurations to get you started. You can also install ROS packages individually.

In case of problems with the next step, you can use following repositories instead of the ones mentioned above [ros-shadow-fixed](http://wiki.ros.org/action/show/TestingRepository?action=show&redirect=ShadowRepository)

* **Desktop-Full Install:** (**Recommended**) : ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators and 2D/3D perception
    ```
    sudo apt install ros-melodic-desktop-full
    ```
* **Desktop Install:** ROS, rqt, rviz, and robot-generic libraries
    ```
    sudo apt install ros-melodic-desktop
    ```
* **ROS-Base:** (Bare Bones) ROS package, build, and communication libraries. No GUI tools.
    ```
    sudo apt install ros-melodic-ros-base
    ```

* **Individual Package**: You can also install a specific ROS package (replace underscores with dashes of the package name):
    ```
    sudo apt install ros-melodic-PACKAGE
    ```
    e.g.
    ```
    sudo apt install ros-melodic-slam-gmapping
    ```
**To find available packages, use:**
```
apt search ros-melodic
```
## Step5: Environment setup
It's convenient if the ROS environment variables are automatically added to your bash session every time a new shell is launched:
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
*If you have more than one ROS distribution installed, ~/.bashrc must only source the setup.bash for the version you are currently using.*

If you just want to change the environment of your current shell, instead of the above you can type:

```
source /opt/ros/melodic/setup.bash
```
If you use zsh instead of bash you need to run the following commands to set up your shell:
```
echo "source /opt/ros/melodic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```
## Step6: Dependencies for building packages
Up to now you have installed what you need to run the core ROS packages. To create and manage your own ROS workspaces, there are various tools and requirements that are distributed separately. For example, rosinstall is a frequently used command-line tool that enables you to easily download many source trees for ROS packages with one command.

To install this tool and other dependencies for building ROS packages, run:
```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
### **Step6.1: Initialize rosdep**

Before you can use many ROS tools, you will need to initialize rosdep. rosdep enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS. If you have not yet installed rosdep, do so as follows.
```
sudo apt install python-rosdep
```
With the following, you can initialize rosdep.
```
sudo rosdep init
rosdep update
```
#
### **Note:**
1. During the installation process, errors may occured. This part will cover some possible ones. When using the command
    ```
    sudo apt install ros--desktop-full
    ``` 
    get error:
    ```
	  E: Could not get lock /var/lib/dpkg/lock-frontend - open(11: Resource temporarily unavailable)
	  E: Unable to aquire the dpkg frontend lock
    ```
    This is due another process getting stuck or currently running

    **Solution:** Check running processes containing "apt" with:
    ```
    ps aux | grep [a]pt
    ```
    Wait a bit and check again if the process is still running or not. It could just be running and not stuck! If the process is stuck, try killing it (The process ID is the first number on the output) with:
    ```
    sudo kill -9 <process_id>
    ```
2. Some packages I see are necessary(Copy - Paste below):
    
    2.1. Update Python to 3.6 or 3.7(2.7 EOL on January 1st, 2020)
    
    * STEP 2.1.1: Install ppa
        ```
        sudo apt update
        sudo apt upgrade
        sudo add-apt-repository ppa:deadsnakes/ppa
        ```
        Update packages
        ```
        sudo apt-get update
        ```

    * Step 2.1.2: Upgrade python 2.x to python 3.x
        
        Before install 3.7, we should have to install python 3.6 by running the following command.
        ```
        sudo apt-get install python3.6
        sudo apt-get install python3.7
        ```
    * Step 2.1.3: PiP installation
        ```
        sudo apt install python3-pip
        ```
    * Step 2.1.4: Set priority
        ```
        sudo update-alternatives — install /usr/bin/python3 python3 /usr/bin/python3.6 1
        ```
        ```
        sudo update-alternatives — install /usr/bin/python3 python3 /usr/bin/python3.7 2
        ```
    
        After that,

        ```
        sudo apt install python-pip
        sudo apt install libhdf5-serial-dev hdf5-tools
        sudo apt-get install openjdk-8-jdk 
        sudo apt-get install libblas-dev liblapack-dev
        sudo apt-get install libfreetype6-dev pkg-config libpng-dev
        
        pip install pip==9.0.1
        pip install numpy
        pip install panda

        pip install cython
        pip install scipy==1.2.0
        pip install matplotlib
        pip install 'scikit-image<0.15'
    

        sudo pip install -U numpy enum34 grpcio absl-py py-cpuinfo psutil portpicker six mock requests gast h5py astor termcolor protobuf keras-applications keras-preprocessing wrapt google-pasta

        pip install keras --user
        ```
3. Udate soon...
