[![Udacity - Robotics NanoDegree Program](https://s3-us-west-1.amazonaws.com/udacity-robotics/Extra+Images/RoboND_flag.png)](https://www.udacity.com/robotics)

# ROS Simple Arm Simulation

<p align="center"><img src="misc/simple_arm.png"></p>

A mini-project to better explain pub-sub architecture in ROS (kinetic)

### How to clone the repository

From your ubuntu home directory run the following command:

```bash
$ git clone https://github.com/mkhuthir/RoboND-ROS-Intro-Simple-Arm.git catkin_ws
```

### How to Launch the simulation?
Make sure you have all the required ROS packages installed, and that this package is in your ROS workspace (assumed to be `~/catkin_ws`.

```sh
$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
```

If you have not built your workspace do it now (make sure you are inside the workspace root  directory):
```sh
$ catkin_make
```

Once the `simple_arm` package has been built, you can launch the simulation environment using:

```sh
$ source ~/catkin_ws/devel/setup.bash
$ roslaunch simple_arm robot_spawn.launch
```
**Please note that if you are having trouble with roslaunch simple_arm robot_spawn.launch please try the safe_spawner.sh script in the scripts folder. You can launch by using $ ./safe_spawner.sh in a terminal of your choice**


Robot can be controlled by publishing joint values to joint controller topics:

```
/simple_arm/joint_1_position_controller/command
/simple_arm/joint_2_position_controller/command
```
In a separate terminal type this command to control joint_1:
```sh
$ rostopic pub -1 /simple_arm/joint_1_position_controller/command std_msgs/Float64 "data: 1.5"
```

To control joint_2:
```sh
$ rostopic pub -1 /simple_arm/joint_2_position_controller/command std_msgs/Float64 "data: 1.5"
```

**Note: Change the value of "data" argument to change joint_position values.**

Another way to change joint values is to call `arm_mover/safe_move` service:

```sh
$ rosservice call /arm_mover/safe_move "joint_1: 0 
joint_2: 0"
```

### How to view image stream from the camera?

Camera image stream is published to following topic:
```
/rgb_camera/image_raw
```

This stream can be viewed by following command in separate terminal:
```sh
$ rosrun image_view image_view image:=/rgb_camera/image_raw
```

If you encounter an error and gazebo crashes while vieweing camera stream, you need to upgrade gazebo7 to gazebo7.6:
```sh
$ sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
$ wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get install gazebo7
```

### Test Video

[![test video](http://img.youtube.com/vi/jaN3Ypqf9sA/0.jpg)](http://www.youtube.com/watch?v=jaN3Ypqf9sA)
