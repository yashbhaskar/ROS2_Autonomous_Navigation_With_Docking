# ROS2_Autonomous_Navigation_With_Docking
This ROS 2 workspace includes packages: a complete robot URDF with Gazebo sensors and plugins, and a Nav2-based autonomous navigation system with SLAM Toolbox localization, Docking Server, and STVL 3D layer. Custom launch files integrate navigation, localization, docking, and map server for full autonomy.

---

## 🟡 Concept of Docking Server

The **Docking Server** in ROS 2 is responsible for enabling a robot to autonomously approach and align with a charging station or docking platform. It integrates with Nav2 and uses sensor feedback (LiDAR, camera, or fiducial markers) to precisely position the robot for physical contact. The docking server receives a docking action request and generates a controlled motion sequence while continuously correcting the robot's pose to ensure accurate alignment. This enables fully automated charging and hands-free operation in long-running missions.

## 🔵 Concept of Undock

The **Undock** action allows the robot to safely and smoothly leave the charging dock after a successful power connection or when a new navigation goal is assigned. The undocking process involves executing predefined backward or rotational maneuvers ensuring that the robot disengages without collisions or sensor blind spots. Once completed, control is handed back to Nav2, enabling the robot to resume autonomous navigation tasks.

<img width="1852" height="1049" alt="1" src="https://github.com/user-attachments/assets/e69f6163-7767-4e08-9aab-f988702325e9" />

---

## 🚀 Features

- Complete Robot URDF Model with sensors (Lidar, IMU, RGB-D Camera, Odometry) and Gazebo plugins
- Nav2 Autonomous Navigation with global & local planners, costmaps, recovery behaviors
- SLAM Toolbox Localization for real-time mapping and pose estimation
- Docking Server Integration for autonomous docking and undocking workflows
- STVL 3D Layer (Spatio-Temporal Voxel Layer) for advanced 3D obstacle perception
- Custom Navigation Launch System including Nav2, SLAM, Map Server & Docking in a single launch
- Gazebo Simulation Support with full robot & sensor visualization in RViz
- Ready for Real Robot Deployment with modular configuration and parameter tuning

---

## 🎓 Learning Objectives

- Build and visualize a robot URDF with sensors and plugins in Gazebo and RViz
- Configure and launch Nav2 for autonomous navigation with path planning and obstacle avoidance
- Perform localization using SLAM Toolbox and understand map publishing/consumption
- Use SLAM Toolbox in localization mode to accurately estimate robot pose
- Integrate the Docking Server to automate robot charging operations
- Use Undock behavior to safely exit the docking station and return to navigation
- Apply STVL 3D costmap layer for enhanced obstacle detection in dynamic environments
- Deploy mapping, localization & navigation pipelines from simulation to real hardware

---

## Installation

### Make Workspace
```bash
mkdir robot_ws/
```

### Change Workspace
```bash
cd robot_ws
```

### Make src
```bash
mkdir src/
```

### Change Workspace
```bash
cd src
```

### Clone This Repository
```bash
git clone https://github.com/yashbhaskar/ROS2_Autonomous_Navigation_With_Docking.git
```

### Clone SLAM Toolbox Repository
```bash
git clone -b humble https://github.com/SteveMacenski/slam_toolbox.git
```

### Clone SLAM Toolbox Repository
```bash
git clone -b humble https://github.com/open-navigation/opennav_docking.git
```

### Install Nav2
```bash
sudo apt update
sudo apt install ros-humble-navigation2
sudo apt install ros-humble-nav2-bringup
```

### (Optional recommended packages)
```bash
sudo apt install ros-humble-nav2-common
sudo apt install ros-humble-nav2-map-server
sudo apt install ros-humble-nav2-behavior-tree
```

### Setup SLAM Localization

- Refer following package to setup SLAM Localization.

[SLAM Localization](https://github.com/yashbhaskar/ROS2_NAV2_With_SLAM_Localization)


### Change Workspace
```bash
cd ..
```

### Build the Package
```bash
colcon build --packages-select my_bot robot_navigation slam_toolbox opennav_docking
source install/setup.bash
```

---

## 🚀 How to Run

### 1st Terminal : Launch robot in gazebo
```bash
ros2 launch my_bot gazebo.launch.py
```

### 2nd Terminal : Start autonoumous navigation
```bash
ros2 launch robot_navigation slam_toolbox_localization.launch.py
```
- Now rviz is open and robot spawn in robot’s initial pose on the map and start SLAM localization.
- Then use Nav2 Goal / 2D Goal Pose to send a navigation goal. The robot will autonomously plan a path and move toward the target, avoiding obstacles and reaching the goal successfully.
- With SLAM Toolbox Localization, you will observe highly accurate pose estimation with minimal to no odometry drift, thanks to loop closure and pose graph optimization, which continuously refines the robot’s position on the map for precise localization.

### 3rd Terminal : Configure & Activate Docking Server
```bash
ros2 lifecycle set /docking_server configure
ros2 lifecycle set /docking_server activate
```

### Verify Docking Actions Available
```bash
ros2 action list
```
- You should see:

```bash
/dock_robot
/undock_robot
```

### Start Docking
```bash
ros2 action send_goal /dock_robot opennav_docking_msgs/action/DockRobot "{dock_id: 'dock1'}"
```

<img width="1852" height="1049" alt="2" src="https://github.com/user-attachments/assets/6bc1ff56-b6e5-45aa-bc63-b15084a39d3f" />

<img width="1852" height="1049" alt="3" src="https://github.com/user-attachments/assets/fbbca261-6aef-4fe2-8074-90772626e2c6" />

---

## ✉️ Contact

📧 Yash Bhaskar – ybbhaskar19@gmail.com

📌 GitHub: https://github.com/yashbhaskar
