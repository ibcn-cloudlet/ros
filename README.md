#ROS catkin workspace

This repository contains all additional ROS packages (besides ROS-desktop) that are used to interface with our robots (Youbot), both in real and simulated environments.

## How to build?

Make sure ROS is installed. I have used and tested it solely with ROS Indigo. The content of this repository should come in the src directory of your catkin workspace.

First source the ROS environment variables, e.g. if you have installed ROS indigo via apt-get:

```
$ source /opt/ros/indigo/setup.bash
```

Next, create a directory for your catkin workspace and clone this repo

```
$ mkdir -p /dir/of/your/choice/catkin_ws/
$ cd /dir/of/your/choice/catkin_ws
$ git clone https://github.ugent.be/e-p/ros.git src
```

Now initialize and build the catkin workspace

```
$ cd src
$ catkin_init_workspace
$ cd ..
$ catkin_make
```

If you now source the setup.bash file created in the devel subdirectory this workspace is overlayed on top of your environment

```
$ source devel/setup.bash
```

Now you should be able to run all ROS packages that are built in this environment


## Sources

Most of the ROS packages are sourced from remote git repositories as submodules. In case we provide patches, we can point these to our own forks of these repositories.

Should we develop any ROS packages from source, or source any code that is not available on git, this can be added into the repository. For example the vrep plugin pakcages are sourced from VREP v3.3.0
