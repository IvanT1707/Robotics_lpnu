# Lab 2: Introduction to ROS2 and Simulation Environment

## Learning Goals

1. Understand fundamental ROS2 concepts (nodes, topics, services, packages)
2. Create a basic ROS2 Python package
3. Launch Gazebo from ROS2 using launch files
4. Use `ros_gz_bridge` to connect Gazebo and ROS2 topics
5. Write a ROS2 publisher node to control robot motion
6. Write a ROS2 subscriber node to process LiDAR data
7. Visualize sensor data in RViz2

## Prerequisites
- Ubuntu (native or WSL2)
- Docker installed and configured

## Build and Test

### Build and Start the Environment
Open your terminal in the root directory of this repository and execute the following commands to set up the Docker container:

```bash
# Build the Docker image (only needed the first time)
./scripts/cmd build-docker

# Start and enter the Docker container
./scripts/cmd run
```

### Build the Package

```bash
# You should already be at /opt/ws when you enter the container

# Build your package
colcon build --packages-select lab2

# Source the workspace (makes your package visible)
source install/setup.bash
```

**Note:** Every time you modify `package.xml`, `setup.py`, or create new launch files, you must rebuild:
```bash
colcon build --packages-select lab2
source install/setup.bash
```

### If You Need to Clean and Rebuild

```bash
# Clean workspace
rm -rf ./build ./install ./log

# Rebuild everything
colcon build

# Or rebuild only lab2
colcon build --packages-select lab2

# Don't forget to source!
source install/setup.bash
```

### Launch Everything

```bash
ros2 launch lab2 gazebo_ros2.launch.py
```

**You should see:**
- Gazebo window with robot and obstacles
- RViz2 window with LiDAR visualization
- Both running together

### Test the Controller (New Terminal)

```bash
./scripts/cmd bash
source /opt/ws/install/setup.bash

# Run the robot controller
ros2 run lab2 robot_controller
```

**Watch the robot move in a sinusoidal pattern!**

### Test the Subscriber (Another New Terminal)

```bash
./scripts/cmd bash
source /opt/ws/install/setup.bash

# Run the LiDAR subscriber
ros2 run lab2 lidar_subscriber
```

**Watch the console for LiDAR statistics and obstacle warnings!**

---

## Explore ROS2 Tools

### List and Inspect Nodes

```bash
# See all running nodes
ros2 node list

# Get detailed info about a node
ros2 node info /robot_controller
ros2 node info /lidar_subscriber
```

### List and Inspect Topics

```bash
# ROS2 topics
ros2 topic list

# Gazebo topics (for comparison)
gz topic -l

# See who's publishing/subscribing
ros2 topic info /cmd_vel
ros2 topic info /lidar

# See message structure
ros2 interface show geometry_msgs/msg/Twist
ros2 interface show sensor_msgs/msg/LaserScan

# View messages in real-time
ros2 topic echo /cmd_vel
ros2 topic echo /lidar --once
```

### Publish Manually

```bash
# Control robot from command line
ros2 topic pub /cmd_vel geometry_msgs/msg/Twist \
  "{linear: {x: 0.5}, angular: {z: 0.0}}" -r 10

# Press Ctrl+C to stop
```

## Troubleshooting

### "Package not found"

```bash
# Make sure you built the package
cd /opt/ws
colcon build --packages-select lab2

# Source the workspace
source install/setup.bash
```

### Bridge not connecting

```bash
# Check topics on both sides
ros2 topic list | grep lidar
gz topic -l | grep lidar

# Check bridge node
ros2 node info /parameter_bridge
```

### RViz2 shows no data

- Fixed Frame must match sensor frame
- Topic must be `/lidar` (check spelling)
- LaserScan display must be enabled (checkbox)
- Check QoS settings if using modified nodes

### Permission denied on Python files

```bash
chmod +x /opt/ws/src/code/lab2/lab2/*.py
```

---