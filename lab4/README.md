# Laboratory Work 4: Dead Reckoning

## Overview
This repository contains the solution for Lab 4. It explores the concept of **Dead Reckoning** — estimating a robot's position by mathematically integrating its velocity commands (`/cmd_vel`) over time.

### Step 1: Build the Workspace
Inside the Docker container, compile the `lab4` package (and `lab3` since we use its movement scripts) and source the workspace:

```bash
cd /opt/ws
colcon build --packages-select lab3 lab4
source install/setup.bash
```

### Step 2: Launch Simulation (Terminal 1)
Launch the TurtleBot3 room environment, the dead reckoning node, the path publisher, and RViz2 for visualization:

```bash
ros2 launch lab4 dead_reckoning_bringup.launch.py
```

### Step 3: Run Trajectory (Terminal 2)
Open a new terminal, enter the container (./scripts/cmd bash), source the setup file, and run the circle trajectory:

```bash
source /opt/ws/install/setup.bash
ros2 run lab3 circle_path
```

## Key Implementations
- dead_reckoning.py: A custom ROS2 node that subscribes to /cmd_vel and calculates the robot's pose using standard differential drive kinematics equations ($x += v \cdot \cos(\theta) \cdot dt$, etc.). It publishes the calculated path to /path_dr.

- Initial Pose Synchronization: To ensure an accurate comparison, the dead reckoning node waits for the first /odom message to sync its mathematical starting position with the robot's actual physical position in Gazebo.

## Observations: Understanding Drift
When running the simulation, you will observe two lines in RViz2:

- Green Line (/path): The ground truth path from Gazebo's odometry.

- Red Line (/path_dr): The mathematically estimated path (Dead Reckoning).
