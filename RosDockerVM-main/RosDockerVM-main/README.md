Today we are going to go implement the mini rover from the last 3 weeks in simulation using ROS, the robot operating system which we will be using throughout the rest of the semester. 

At a high level, the two important concepts we will use are ros topics and nodes. Nodes are components within ros that are responsible for performing tasks by executing arbitrary code, for example, we might have a node to control a wheel in the rover. Nodes communicate with other nodes using topics, which they can publish messages or subscribe to. 

For more information, look at:
- https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html#
- https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Topics/Understanding-ROS2-Topics.html
Or a great tutorial series by the channel articulated robotics here: 
https://beta.articulatedrobotics.xyz/tutorials/ready-for-ros/ros-overview

To build the simulation today, we need a ros environment, there are many ways to do this, but for today, the simplest approach should be using a docker container. 

Make sure you have docker installed, which can be downloaded from here: https://hub.docker.com/welcome

Then, download or clone this github repository and run: 
```sh
docker compose up --build
```
And open the url: http://localhost:6080 which should open a linux virtual environment. 

Within this virtual environment open two terminal windows, and run: 
```sh
ros2 run demo_nodes_cpp talker
```
In one terminal, and in the other,
```sh
ros2 run demo_nodes_cpp listener
```

If both terminals display the same messages, congratulations, you have successfully installed ros!

Now, we can start working on trying to implement the simulation. 
