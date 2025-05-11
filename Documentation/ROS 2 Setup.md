# ROS 2 Humble Installation on Ubuntu

Official ROS 2 Humble installation steps for Ubuntu, adapted from [docs.ros.org](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html#setup-sources).

---

## Set Locale

Make sure your system supports `UTF-8`. If you're in a minimal environment (like Docker), the locale may default to `POSIX`.

```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

---

## Setup Sources

### Enable the Universe Repository

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

### Add the ROS 2 GPG Key

```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

### Add the ROS 2 Repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## Install ROS 2 Packages

### Update your apt cache

```bash
sudo apt update
```

### Upgrade your system (recommended)

```bash
sudo apt upgrade
```

### Desktop Install (Recommended)

Includes ROS, RViz, demos, tutorials, etc.

```bash
sudo apt install ros-humble-desktop
```

### Development Tools (optional)

```bash
sudo apt install ros-dev-tools
```

---

## Environment Setup

### Source the setup script

```bash
source /opt/ros/humble/setup.bash
```

To automatically source it on every terminal session:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## ROS 1 Bridge (Optional)

Allows communication between ROS 1 and ROS 2 topics.

Link: [ROS 1 Bridge GitHub](https://github.com/ros2/ros1_bridge/blob/master/README.md)

---

## Uninstall Instructions

To remove ROS 2 Humble packages:

```bash
sudo apt remove ~nros-humble-* && sudo apt autoremove
```

To remove the repository:

```bash
sudo rm /etc/apt/sources.list.d/ros2.list
sudo apt update
sudo apt autoremove
sudo apt upgrade
```

---

> Tip: Always refer to the [official documentation](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html) for any updates.
