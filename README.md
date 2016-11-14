#ROS catkin workspace

This repository contains all additional ROS packages (besides ROS-desktop) that are used to interface with our robots (Youbot), both in real and simulated environments.

## How to build?

Make sure ROS is installed. I have used and tested it solely with ROS Indigo. The content of this repository should come in the src directory of your catkin workspace.

To build the catkin workspace catkin tools is required (for the vrep plugin): http://catkin-tools.readthedocs.io/en/latest/verbs/catkin_build.html

Installing ROS Indigo on Ubuntu 14.04 goes like this:

```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net --recv-key 0xB01FA116
$ sudo apt-get update
$ sudo apt-get install ros-indigo-desktop-full
$ sudo rosdep init
$ rosdep update
$ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
$ sudo apt-get install python-rosinstall
$ sudo apt-get install python-catkin-tools
```

First source the ROS environment variables, e.g. if you have installed ROS indigo via apt-get:

```
$ source /opt/ros/indigo/setup.bash
```

Next, create a directory for your catkin workspace and clone this repo

```
$ mkdir -p /dir/of/your/choice/catkin_ws/
$ cd /dir/of/your/choice/catkin_ws
$ git clone https://github.ugent.be/e-p/ros.git src
$ cd src
$ git submodule init
$ git submodule update
```

Now initialize and build the catkin workspace

```
$ cd src
$ catkin_init_workspace
$ cd ..
$ catkin build --continue-on-failure
```

Continue on failure is required since some (unrequired) dependency packages will not build.

If you now source the setup.bash file created in the devel subdirectory this workspace is overlayed on top of your environment

```
$ source devel/setup.bash
```

Now you should be able to run all ROS packages that are built in this environment


## Sources

Most of the ROS packages are sourced from remote git repositories as submodules. In case we provide patches, we can point these to our own forks of these repositories.

Should we develop any ROS packages from source, or source any code that is not available on git, this can be added into the repository. For example the vrep plugin pakcages are sourced from VREP v3.3.1

## VREP plugin

We use the latest VREP ROS interface to communicate with ROS from VREP scripts. The source of the plugin is found in the programming/ folder of VREP. 

For the YouBot, make sure also to include the following messages in meta/messages.txt

```
brics_actuator/Poison
brics_actuator/JointValue
brics_actuator/JointPositions
brics_actuator/JointVelocities
brics_actuator/JointTorques
```

This is already set up since we included these files in our git repository.

After building copy the file devel/lib/libv_repExtRosInterface.so to your vrep installation directory.

## Additional libraries

* openni_camera has to be linked against log4cxx, install the package `sudo apt-get install liblog4cxx-dev`

* problems with Xtion Pro on Linux, fix by upgrading firmware of device: https://github.com/nh2/asus-xtion-fix

* joy ros package requires the joystick package to be installed on Ubuntu: ` sudo apt-get install joystick`
