## Prerequisites

- **Ubuntu 24.04** (native, WSL2, dual boot, or VirtualBox)
- **Git** and **GitHub account** - [GitHub Hello World Guide](https://docs.github.com/en/get-started/start-your-journey/hello-world)
- **30 GB free disk space**
- **8 GB RAM** (16 GB recommended)

**Don't have Ubuntu 24.04?** See the [Installation Guide](docs/INSTALLATION_GUIDE.md) for setup instructions.

---
### 1. Clone Repository

```bash
cd ~
git clone https://github.com/IvanT1707/Robotics_lpnu.git
cd robotics_lpnu
```

### 2. Build Docker Image

```bash
./scripts/cmd build-docker
```

This takes 10-15 minutes on first run.

### 3. Run Container

```bash
./scripts/cmd run
```

### 4. Testing Robot

```bash
# Run Container
./scripts/cmd run
```

```bash
# Open another terminal
./scripts/cmd bash

# Launch Gazebo with your robot world in the first terminal
gz sim /opt/ws/src/code/lab1/worlds/robot.sdf

# In another terminal, list topics
gz topic -l

# Look at the lidar messages on the /lidar topic, specifically the ranges data
gz topic -e -t /lidar


# Send movement command
gz topic -t "/cmd_vel" -m gz.msgs.Twist -p "linear: {x: 0.5}, angular: {z: 0.2}"
```


**Test movement:**
- Activate Key publisher plugin inside the Gazebo GUI to use your keyboard arrows to drive the robot. 
- Publish to `/cmd_vel` topic
