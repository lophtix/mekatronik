Update:  
```
sudo apt-get update
sudo apt-get upgrade
```
  
Setup with raspi-config:  
```sudo raspi-config```  
  
**Network Options:**
* Hostname > set hostname to rosberrypi2.X  
* Wi-Fi > connect to wi-fi  

**Boot Options:**  
* Desktop / CLI > select *Console Autologin*  
* Splash Screen > turn off splash screen  

**Localisation Options:**  
* Change Keyboard Layout > set keyboard layout to Swedish  

**Interfacing Options:**  
* Camera > enable camera  
* SSH > enable SSH  

**Advanced Options:**  
* *Expand Filesystem*  
  
Install pijuice software and remove lock file:
```
sudo apt-get pijuice-base
sudo rm /tmp/pijuice_gui.lock
```  
  
Install ROS Kinetic:
```
sudo apt-get install dirmngr

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

sudo apt-get install -y python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential cmake

sudo rosdep init
rosdep update

mkdir -p ~/ros_catkin_ws
cd ~/ros_catkin_ws
```  
Choose one:
ROS-Comm (No GUI)
```
rosinstall_generator ros_comm --rosdistro kinetic --deps --wet-only --tar > kinetic-ros_comm-wet.rosinstallwstool init src kinetic-ros_comm-wet.rosinstall
```
OR:  
Desktop (GUI)
```
rosinstall_generator desktop --rosdistro kinetic --deps --wet-only --tar > kinetic-desktop-wet.rosinstall
wstool init src kinetic-desktop-wet.rosinstall
```
