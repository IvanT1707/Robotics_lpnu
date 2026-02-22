# Robotics Introduction Labs

Hands-on labs for learning ROS2 and robotics simulation with Gazebo.

---

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
### 4. Install and open VScode

```bash
code .
```


#### Open Additional Terminals

```bash
# In a new terminal window
./scripts/cmd bash
```
---