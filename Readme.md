# Mir_navigation_customized_docker
Usage MIR robot with customized navigation package in docker 

# Agenda

- [Prerequisites](#prerequisite)
    - [Docker Installation](#docker-installation)
    - [Docker Setup](#docker-setup)
- [Navigation Running](#navigation-running)

## **Prerequisites**

> Note: If you have already done prerequisite, you may move to [Navigation step](#navigation-running).

### **_Docker Installation_**

> Note: If you have already installed Docker, you may skip this step.

#### _For Windows_

[Windows Installation](https://docs.docker.com/desktop/install/windows-install/)

#### _For Ubuntu_

[Ubuntu Installation](https://docs.docker.com/engine/install/ubuntu/)

### **_Xlaunch Installation_**

> Note: If you have already installed Xlaunch, you may skip this step.

[Xlaunch Installation](https://sourceforge.net/projects/xming/)

### **_Docker Setup_**

> Note: If you have already setup Docker, you may skip this step.

#### _Docker basic command_

- `docker ps` > It will show list of docker running.

- `docker ps -a` > It will show list of docker running in background.

- `docker images` > It will show list of images available on the system.

- `docker start ($image_name or $image_ID)` > It will start the particular image on the docker.

- `docker stop ($image_name or $image_ID)` > It will stop the particular image on the docker.

- `docker run -it --name $any_name $images bash` > It will start the particular image on the new docker.

- `docker exec -it ($image_name or $image_ID) bash` > It will open the image which was already running.

#### _Docker GUI_

> Note: If you have already installed Xlaunch, you may continue this step or you can to [Xlaunch installation](#xlaunch-installation)

- `docker run --name $any_name -e DISPLAY=host.dcoker.internal:0.0 -it $image_name` > It will display the GUI for docker.

#### _Docker pull image_

`docker pull osrf/ros:noetic-desktop-full`

&nbsp; It will pull the ros noetic image from online.

#### _Docker ros noetic prerequisites_

- For first initialization,

    `docker run --name mir_robot -e DISPLAY=host.docker.internal:0.0 -v path/to/volume/mir_robot_docker:/Home -it osrf/ros:noetic-desktop-full`

    `path/to/volume => location address where u downloaded the mir_robot_docker file`

It will start and run the docker with the given image and volume specified for it. For closing, type `exit` and `enter` on the terminal.

- After that, now start the docker with the image_name.

    `docker start mir_robot`

    `docker exec -e DISPLAY=host.docker.internal:0.0 -it mir_robot bash`

It will open the docker with the image_name. For closing, type `exit` and `enter` on the terminal.

- change the directory to the workspace directory.

    `cd Home/mir_ws/src`

- create `catkin_init_workspace` on source

    `catkin_init_workspace`

- change the directory to the workspace directory.

    `cd ..`

- Install the  `requirement.sh` file on the docker, using

    `sudo apt-get update`
    
    `sudo apt-get -y upgrade`
    
    ``` Install dependencies
    sudo apt-get -y install ros-noetic-costmap-queue \
    ros-noetic-dwb-critics \
    ros-noetic-rospy-message-converter \
    ros-noetic-sbpl-lattice-planner \
    ros-noetic-dwb-plugins \
    ros-noetic-move-base \
    ros-noetic-amcl \
    ros-noetic-teb-local-planner \
    ros-noetic-map-server \
    ros-noetic-fake-localization \
    ros-noetic-robot-localization
    ```

- change the directory to the workspace directory.

    `cd Home/mir_ws`

- do the `catkin_make` at the workspace

    `catkin_make`

- Now, stop the docker with the image_name.

    `docker stop mir_robot`

## **Navigation Running**

> Note: I have named the docker as `mir_robot`, you can change name as per your requirement.

- Start the docker with the image_name.

    `docker start mir_robot`

    `docker exec -e DISPLAY=host.docker.internal:0.0 -it mir_robot bash`

- change the directory to the workspace directory.

    `cd Home/mir_ws`

- source the workspace directory.

    `source devel/setup.bash`
  
- export XDG Runtime dir for dcoker

    `export XDG_RUNTIME_DIR=/path/to/workspace/mir_ws`
  
- launch the navigation file along with simulation file.

    `roslaunch mir_navigation_customized mir_navigation_customized.launch`

    > Note: Now, I have used fake localization for the navigation. We can able to change the localization to the amcl localization through uncomment amcl on the `mir_navigation_customized.launch` file and comment out fake localization.

- Now, you can give the `2d Nav goal` for the autonmous navigation.

- For closing `ctrl + c` and type `exit` and `enter` on the terminal.

- Now, stop the docker with the image_name.

    `docker stop mir_robot`

<p style="text-align: center;"><b><i>--The end--</i></b></p>
