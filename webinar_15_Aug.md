# ROS 2 & Robotics Dev Workflow – From Basics to Real-World Simulation

## Introduction to ROS 2 and Robotics Development

**Welcome everyone. Today’s session will take you through a journey of building and simulating intelligent robots using ROS 2 — a modern, industrial-grade robotics middleware. Robotics is evolving rapidly across industries, and ROS 2 is at the center of this revolution.**
**Let’s start with a basic question:**

**What powers a robot's brain?**

***Just like humans need a nervous system to sense, think, and act — robots need a middleware to connect sensors, decisions, and motors. That middleware is called ROS, short for Robot Operating System.***

* **ROS 2 is not a software you install and “run.”**

* **It’s a framework that connects different parts of a robot.**

**Robots are no longer restricted to factories. They’re in hospitals assisting surgeries, in warehouses automating logistics, on roads powering autonomous cars, and even exploring other planets. And almost all of these use ROS2 as a backbone for software development.**

**Real-World Examples:**

* **Autonomous Vehicles (e.g., Tier IV, OpenADKit, Autoware): ROS 2 is used for perception, planning, and control.**

![ADAS_ROS](media/ADAS_ROS.jpg)


![Starship Delivery Robots](media/starship1.jpg)


![Starship Delivery Robots](media/starship2.jpeg)

* **Medical Robotics (e.g., Accuray CyberKnife, Stryker): Simulation and planning using Gazebo + ROS.**

![Surgical Robots](media/Medical_robots.avif)

* **Warehouse Automation (e.g., Amazon Robotics, Locus Robotics): ROS 2 used for navigation and fleet management.**

![Amazon Robots](media/amazon_robot.avif)

* **Space Exploration (e.g., NASA’s VIPER rover): Uses ROS and Gazebo for mission simulation and autonomy testing.**

![NASA VIPER](media/NASA_Viper.webp)


## Key Concepts in ROS 2

**ROS 2 is a flexible, open-source framework for writing robot software. It enables communication between different parts of a robot or between multiple robots. Let's understand a few core concepts:**

### 1. ROS2 Workspace

**First of all let's create a ROS2 workspace. But wait… do you know what a workspace is in ROS? 🤔**

**Let’s break it down!**

**In ROS (Robot Operating System), a workspace is a dedicated directory where you develop, build, and manage ROS packages. It acts as an isolated environment, helping you organize and compile your ROS projects efficiently.**

**Now that we understand what a workspace is, let’s create one! 🚀**

```bash
mkdir -p ros2_ws/src
```
**Now confirm if the directory is created or not**
```bash
ls
```

**🎉 Congratulations! You've just created your first ROS 2 workspace in your home directory, named ros2_ws.**

**Now navigating inside the ros2_ws directory and again listing the files/folders inside**
```bash
cd ros2_ws
ls
```

***The src (source) folder is where you'll create and store all your ROS 2 packages in the future. Think of it as the heart of your workspace, where all the magic happens! ✨***

### 2. Setup the ROS Environment

**So, we learned how to create a workspace to store our code and packages. Now, it's time to set up the environment! 🚀**

**But wait… do you have any questions? 🤔**

**Why is this step necessary?**

**Setting up the ROS 2 environment allows us to source the setup files, enabling us to use ROS 2 commands. This is a crucial step, without it, ROS 2 won’t recognize your commands!**

**So for every terminal you open, run the following command**
```bash
source /opt/ros/jazzy/setup.bash
```
***It's frustrating to run everytime the above command for every terminal we open***

**So to automate, add the above command in the `.bashrc` file as follows:**
```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
**Great! We can directly execute the ROS2 commands and will save our time.**

**Now to confirm if everything setup correctly, run**
```bash
printenv | grep -i ROS
```

### 3. ROS2 Graph

**The ROS Graph is like a map of all processes (nodes) and how they communicate — topics, services, actions.**

> 🧠 **Think of it like a circuit diagram**: each node is a component, and the wires are topics/services/actions connecting them.

* **Node**: A node is a single software module that performs computation. In robotics, each sensor, actuator, or function is typically handled by a separate node.


* **Topic**: Topics are used for streaming data between nodes. One node publishes data to a topic, and another node subscribes to it.


* **Service**: Used for a one-time request-reply interaction, like asking a sensor for a reading.


* **Action**: Handles long-running tasks like robot arm movement or autonomous navigation goals.

* **Parameters**: Store and manage configuration settings during runtime.

* **Launch File**: A script that launches multiple nodes together, often with configuration.

**To reinforce what we've learned so far about ROS 2 graph, here's a simple diagram showing how nodes communicate through topics and services as well as actions.**

![ROS 2 Node Communication](media/Nodes-TopicandService.gif)

![ROS2 Action](media/action.gif)

📘 View source: [ROS 2 Node Tutorial (Jazzy)](https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)

**ROS 2 ensures your robot's brain, eyes, arms, and decision-making can all work together seamlessly.**

**Let's take up real-life example to get a clear glimpse of ROS2 graph**

![Cricket Topic](media/cricket_topic.png)

![Cricket Service](media/cricket_service.png)

![Cricket Action](media/cricket_action.png)

## Demo of Turtlesim Simulator:

**Let’s now see ROS 2 in action using a classic demo tool – `Turtlesim`, a 2D robot simulator.**

**🐢 Turtlesim**

    A lightweight simulator to learn ROS 2 basics like nodes, topics, and movement — simple, but very powerful for grasping core ideas.

**🔧 `ros2` CLI**

    Command-line interface to control and inspect everything in ROS 2 — from running nodes to reading topics or setting parameters.

**🖥️ rqt**

    Graphical tool that gives you a visual overview and interactive control of the ROS 2 system — great for beginners and debugging.

**Now to check if it's installed**

```bash
ros2 pkg executables turtlesim
```
**It should return the executables of turtlesim**

### Nodes

**`ros2 run`**

**It is used to launch any executable of a packages**

```bash
ros2 run <package_name> <executable_name>
```
🎯 **Goal:** Start the `turtlesim_node`

**Open a terminal**

```bash
ros2 run turtlesim turtlesim_node
```
**👀 What’s happening?**

**Package: `turtlesim`**

**Executable: `turtlesim_node`**

**To control the turtle, in another terminal;**

```bash
ros2 run turtlesim turtle_teleop_key
```
**Package: `turtlesim`**

**Executable: `turtle_teleop_key`**

**Now the turtle can be controlled from keyboard using arrow keys, when this terminal is active only**

**`ros2 node list`**

**Now to see all the nodes associated with the executables**

**In another terminal:**

```bash
ros2 node list
```
**This will list all the active nodes**

**Remapping**

**Remapping allows you to reassign default node properties, like node name, topic names, service names, etc., to custom values.**

**Now, let’s reassign the name of our /turtlesim node as**

```bash
ros2 run turtlesim turtlesim_node --ros-args --remap __node:=tortoise
```
**Now the node listing will also list this renamed node**

**`ros2 node info`**

**To get information of a particular node**

```bash
ros2 node info <node_name>
```
**So let's examine our latest node `tortoise`**

```bash
ros2 node info /tortoise
```
### Topics

**rqt graph**

**It will be used to visualize the changing nodes and topics, as well as the connections between them.**

```bash
rqt_graph
```

**`ros2 topic list`**

**To list all the topics active in the system, run:**

```bash
ros2 topic list
```
```bash
ros2 topic list -t
```
**This will return the same list of topics, this time with the topic type appended in brackets.**

**`ros2 topic echo`**

**To see the data being published on a topic, use:**

```bash
ros2 topic echo <topic_name>
```

**Example**

```bash
ros2 topic echo /turtle1/cmd_vel
```

***To see the data changing live,***

**Move the turtle using the `/teleop_turtle` node**

**`ros2 interface show`** 

**To understand message type, specifically the structure of the data it expects, use:**

```bash
ros2 interface show <msg_type>
```

**Example:**

```bash
ros2 interface show geometry_msgs/msg/Twist
```

***Publishers and subscribers must send and receive the same type of message to communicate over topics***

**`ros2 topic pub`**

**To publish to a topic directly using the message structure:**

```bash
ros2 topic pub <topic_name> <msg_type> '<args>'
```

**Example: To move the turtle continuously:**

```bash
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```

### Services

**A service type defines two things: what you're allowed to ask (the request) and what reply you’ll get (the response). Unlike topics, which use one message, services use two — one for sending the request, and one for receiving the response.**

**`ros2 service list`**

**To list all the active services in the system:**

```bash
ros2 service list
```

**`ros2 service type`**

**To find out the type of a service:**

```bash
ros2 service type <service_name>
```

**Example:**

```bash
ros2 service type /spawn
```

**`ros2 interface show`**

**To know the structure of the input arguments**

```bash
ros2 interface show <type_name>
```

**Example:**

```bash
ros2 interface show turtlesim/srv/Spawn
```

**`ros2 service call`**

**To call a service using the input arguments data structure:**

```bash
ros2 service call <service_name> <service_type> <arguments>
```

**Example:**

```bash
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2.0, y: 2.0, theta: 1.57, name: 'turtle2'}"
```

### Parameters

**`ros2 param list`**

**To see the parameters belonging to active nodes:**

```bash
ros2 param list
```

**`ros2 param get`**

```bash
ros2 param get <node_name> <parameter_name>
```

**Example:**

```bash
ros2 param get /turtlesim background_b
```

**`ros2 param set`**

**To change a parameter’s value at runtime:**

```bash
ros2 param set <node_name> <parameter_name> <value>
```

**Example:**

```bash
ros2 param set /turtlesim background_r 150
```

**Remember the change is only temporary for current session**

### Actions
**`ros2 action list`**

**To list all the actions**

```bash
ros2 action list
```

**`ros2 action type`**

**For seeing action type:**

```bash
ros2 action type /turtle1/rotate_absolute
```

**`ros2 interface show`**

**Structure of action type:**

```bash
ros2 interface show turtlesim/action/RotateAbsolute
```

**`ros2 action send_goal`**

**To send an action goal:**

```bash
ros2 action send_goal <action_name> <action_type> <values>
```

**Example: Keep an eye on turtlesim window and run:**

```bash
ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"
```

**To see the feedback of this goal**

```bash
ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: -1.57}" --feedback
```

### Launching nodes

**To start multiple nodes at once using a single file, the launch file in the format filename.launch.py**

**`ros2 launch`**

**In a new terminal:**

```bash
ros2 launch turtlesim multisim.launch.py
```

**In second terminal:**

```bash
ros2 topic pub  /turtlesim1/turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```

**In third terminal:**

```bash
ros2 topic pub  /turtlesim2/turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: -1.8}}"
```

**This simple simulation demonstrates how concepts of ROS 2 are used — from controlling the robot to monitoring its state. Now let's move onto something complex and real ...**

## Demo of custom Carbot using Galaxium:

**Moving beyond simple simulations, let’s now simulate a real-world carbot — `RC Car` — with differential drive, and Gazebo integration, also running on Galaxium.**

**RC Car is our custom-built carbot model for the Galaxium platform. It mimics how autonomous ground robots navigate and perceive their environment.**

**Now source the carbot simulation package `rc_car` as:**

```bash
source install/setup.bash
```

**Note:** ***For every new terminal we need to source install setup of the simulation package***

**To check if installed package `rc_car` is sourced correctly:**

```bash
ros2 pkg executables rc_car
```

**Thus start the `rc_car` package using launch file:**

```bash
ros2 launch rc_car rc_car.launch.py
```

**Now let's understand some nodes & topics of the package `rc_car`**

**In another terminal, run the `circular_path` node:**

```bash
source install/setup.bash
ros2 run rc_car circular_path
```

**In terminal 3 `cmd_vel_listener` node:**

```bash
source install/setup.bash
ros2 run rc_car cmd_vel_listener
```

**In terminal 4 `odom_listener` node:**

```bash
source install/setup.bash
ros2 run rc_car odom_listener
```

**Now let's see the node list. In another terminal 5:**

```bash
source install/setup.bash
ros2 node list
```

**Now let's see the topic list. In the same terminal 5:**

```bash
ros2 topic list
```

***So the nodes are communicating through the topics `/cmd_vel` and `/model/rc_car/Odometry`. And this can be visualized using the `rqt_graph`***

```bash
rqt_graph
```

**Now the info of nodes & topics; types of topics; echo the topics; data structure of the message of each topics interface; publishing data through topics can be done through CLI**

```bash
ros2 node info <node_name>
ros2 topic echo <topic_name>
ros2 topic type <topic_name>
ros2 topic echo <topic_name>
ros2 topic info <topic_name>
ros2 interface show <msg_interface>
ros2 topic pub <topic_name> <msg_type> '<args>'
```

**Example:**
```bash
ros2 topic pub /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```

**Now moving onto services of `rc_car` package**

**Try these for the `rc_car`:**

```bash
ros2 service list
ros2 service type <service_name>
ros2 service info <service_name>
ros2 interface show <srv_interface>
ros2 service call <service_name> <service_type> <arguments>
```

**Example:**

```bash
ros2 service call /world/world_demo/set_pose ros_gz_interfaces/srv/SetEntityPose "{entity: {name: 'rc_car', type: 2}, pose: {position: {x: 1.0, y: 2.0, z: 0.0}, orientation: {x: 0.0, y: 0.0, z: 1.0, w: 1.0}}}"
```

**Now to reset it all we can call the control service as:**

```bash
ros2 service call /world/world_demo/control ros_gz_interfaces/srv/ControlWorld "{world_control: {reset: {all: true}}}"
```

**The parameters of the active nodes can be listed and also other commands are executed as:**

```bash
ros2 param list
ros2 param get <node_name> <parameter_name>
ros2 param set <node_name> <parameter_name> <value>
```

**Dump and load can be used for relevant parameters**

**Now the action of the `rc_car` packages can be understood as:**

**First start the action server `drive_distance_server`**

```bash
ros2 run rc_car drive_distance_server
```

**Now the previous commands for inspecting the action and related nodes can be done:**

```bash
ros2 node list
ros2 node info /drive_distance_server
ros2 action list
ros2 action type /drive_distance
ros2 action info /drive_distance
ros2 interface show rc_car_interfaces/action/DriveDistance
```

**Now based on the type and interface structure of the action, the action goal can be sent through CLI as:**

```bash
ros2 action send_goal <action_name> <action_type> <values>
```

**Example:**

```bash
ros2 action send_goal /drive_distance rc_car_interfaces/action/DriveDistance "{distance_m : 1.3}"
```

**And also we can run the action client as:**

```bash
ros2 run rc_car drive_action_client 2
```

***where 2 is the distance we provide. Also note that action server should be always running to execute an action goal.***


**From begining only we are using the launch file to start our carbot package `rc_car`**


## Robotics Development Workflow

**A robotic system is more than just moving parts. It requires a structured development approach. Here's the typical workflow — and everything demonstrated here runs fully on Galaxium:**

1. **Create Packages**: Code is organized into packages with nodes, messages, and services.
```bash
my_robot_package/
├── package.xml
├── setup.py / CMakeLists.txt
├── resource/
├── my_robot_package/
│   ├── __init__.py
│   ├── publisher_node.py
│   └── subscriber_node.py ...
├── launch/
│   └── model.launch.py
├── config/
│   └── robot_params.yaml ...
├── model/
│   └── model.sdf
|   └── model.config
|   └── meshes/
|   |       └── part1.stl
|   |       └── part2.stl ...
```
2. **Build with Colcon**: ROS 2 uses Colcon to compile multiple packages.
3. **Run with Launch Files**: Launch multiple nodes together with required parameters.
4. **Simulate**: Test your logic in Gazebo, avoiding hardware damage.
5. **Debug with CLI**: Use introspection tools to check health and comms.
6. **Deploy**: Finally, deploy on real robots using Docker or microcontrollers.

**Galaxium integrates this entire workflow into one seamless cloud-based interface.**

## Conclusion

**🚀 What You’ve Seen Today:**

- The power of ROS 2 — beyond Turtlesim and textbooks

- How Gazebo + ROS 2 can simulate real-world robots: `rc_car` package

- A sneak peek into Galaxium — our cloud-based robotics development platform

**🔑 What Comes Next:**


**→ Learn ROS 2 hands-on with simulation and code**

- 🎓 Enroll in the Robotics Onboarding Module (ROM)

**→ Build, test & simulate robots anytime, anywhere**

- 🌐 Subscribe to Galaxium

**🎁 Bonus for Attendees:**

💡 Get exclusive early access & discounts if you register for ROM within 3 days!

**CTA:**

- 👉 Explore Galaxium/ROM at [NextAISense](https://nextaisense.com/)

**Thank you for attending!**