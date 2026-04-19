# Laboratory 7: Coordinate Transforms (TF2), URDF/Xacro, and RTR Manipulator

## Overview
This package contains the implementation of Laboratory 7 for the Robotics (ROS 2) course. It focuses on spatial transforms using the `tf2` library, physical robot modeling using `URDF` and `Xacro`, and verifying the forward kinematics of a 3-DOF Revolute-Translational-Revolute (RTR) manipulator.

## Key Features & Implementations
* **TF2 Broadcasters and Listeners:** Python nodes that publish dynamic transforms and query transforms via a buffer (`tf2_broadcaster_demo.py`, `tf2_listener_demo.py`).
* **URDF & Collision Geometry:** An updated `rtr_manipulator.xacro` file that includes both visual representations and precise `<collision>` tags for physical motion planning.
* **ROS 2 Control Integration:** Launch files to bring up the `joint_state_broadcaster` and `forward_position_controller` using a mock hardware interface.
* **Kinematics Verification:** Analytic mathematical proofs validating that the ROS 2 TF tree perfectly matches the theoretical forward kinematics of the RTR manipulator.

## How to Run

**1. Build the package**
```bash
colcon build --packages-select lab7 --symlink-install
source install/setup.bash
```

**2. Visualize the Robot (RViz2 & Joint Publisher)**
```bash
ros2 launch lab7 rtr_visualize.launch.py
```

**3. Run Controllers and Send Motion Commands**
```bash
# Launch the control nodes
ros2 launch lab7 rtr_ros2_control.launch.py

# In a separate terminal, send a position command [theta_1, theta_2, theta_3]
ros2 topic pub --once /forward_position_controller/commands std_msgs/msg/Float64MultiArray "{data: [0.2, 0.6, 0.4]}"
```