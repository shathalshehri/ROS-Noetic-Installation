# ROS Noetic & ROS Foxy on Ubuntu 20.04 Installation Guide

## 1.1 Installing ROS Noetic on Ubuntu 20.04.3 LTS

In this section, I will show you how to install ROS on the Ubuntu operating system. I’ve already installed Ubuntu 20.04.3 on a Virtual Machine. If you haven't installed VirtualBox on your operating system yet, you can install it using the references below. You will also need to download the Ubuntu ISO from their website.

1. [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. [Download Ubuntu ISO](https://ubuntu.com/download/desktop)

If you encounter any difficulties with the installation process, I recommend following the steps in a YouTube video. Simply type your operating system and what you want to install on it. If you encounter any errors, copy and paste them into your browser to understand the problem and find a solution.

### What is ROS (Robot Operating System)?

ROS stands for Robot Operating System, which is more like an environment. It has the ability to connect nodes together. By nodes, we mean pieces of software that can be written in C++ or Python. They can handle tasks such as reading a sensor or controlling a servo. These nodes connect together using a publisher/subscribe protocol.

### Installing ROS Noetic on Ubuntu

Follow the steps below and enter the commands in the terminal:

1. **Set up the ROS Noetic repository for Ubuntu 20.04**
    ```sh
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
    ![Set up ROS Noetic repository](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/14.png)

2. **Add the official ROS keyring**
    ```sh
    sudo apt install curl # if you haven't already installed curl
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
    ![Add the official ROS keyring](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/15.png)

3. **Update the ROS package index**
    ```sh
    sudo apt update
    ```
    ![Update ROS package index](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/update.png)

4. **Install the ROS Noetic package**
    In most cases, you will want to install `ros-noetic-desktop-full` for a full ROS experience (Recommended).
    ```sh
    sudo apt install ros-noetic-desktop-full
    ```
    ![Install ROS Noetic package](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/19.png)

5. **Verify the Noetic installation**
    You must source this script in every bash terminal you use ROS in:
    ```sh
    source /opt/ros/noetic/setup.bash
    ```
    ![Source setup.bash](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/20.png)

    Then, write `roscore` to make sure that the installation process was successful:
    ```sh
    roscore
    ```
    ![roscore](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/21.png)
   
7. **Install Additional Dependencies for Building ROS Packages**
    To create and manage your own ROS workspaces, you will need additional tools and dependencies. Install the following packages to handle this:
    ```sh
    sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
    ```
    ![Install additional dependencies](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/26.png)

8. **Initialize rosdep**
    Before using many ROS tools, you need to initialize `rosdep`. `rosdep` allows you to easily install system dependencies for source code you want to compile and is required to run some core components in ROS. If you have not yet installed `rosdep`, do so with the following command:
    ```sh
    sudo apt install python3-rosdep
    ```
    ![Initialize rosdep](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/27.png)

    With the following, you can initialize `rosdep`:
    ```sh
    sudo rosdep init
    rosdep update
    ```
    ![rosdep initialization](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/28.png)
---
# 1.2 ROS 2 (Foxy) Installation Guide for Ubuntu 20.04

## ROS 2 Installation on Ubuntu 20.04

This guide provides step-by-step instructions for installing ROS 2 on Ubuntu 20.04. Follow the instructions below to set up your ROS 2 environment.

### Set Locale

Ensure you have a locale that supports UTF-8. If you are in a minimal environment (such as a Docker container), the locale may be minimal like POSIX. We test with the following settings. However, it should be fine if you’re using a different UTF-8 supported locale.

```sh
locale  # check for UTF-8
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # verify settings
```
![Set Locale - Check UTF-8](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/setlocale.png)

### Setup Sources
You need to add the ROS 2 apt repository to your system.

First, ensure that the Ubuntu Universe repository is enabled

```sh
apt install software-properties-common
sudo add-apt-repository universe
```
![Setup Sources - Enable Universe Repository](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/SetUpSources.png)

Add the ROS 2 GPG key with apt.

```sh
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```
![Setup Sources - Add GPG Key](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/ROS2GPGkey-with-apt.png)

Then add the repository to your sources list.


```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
![Setup Sources - Add Repository](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/add-repo-to-sourcesList.png)

### Install ROS 2 Packages
Update your apt repository caches after setting up the repositories.
```sh
sudo apt update
```
![Update apt repository](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/update.png)

ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages.
```sh
sudo apt upgrade
```
![Upgrade system packages](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/upgrade.png)

Desktop Install (Recommended): ROS, RViz, demos, tutorials.
```sh
sudo apt install ros-foxy-desktop python3-argcomplete
```
![Desktop Install](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/Desktop%20Install.png)

### Environment Setup
#### Sourcing the setup script

Set up your environment by sourcing the following file.
```sh
# Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/foxy/setup.bash
```
![Setup Environment](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/SetupEnvironment.png)


### Try Some Examples
If you installed ros-foxy-desktop above, you can try some examples.

In one terminal, source the setup file and then run a C++ talker:
```sh
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_cpp talker
```
![C++ Talker Example](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/example%3Atalker.png)

In another terminal, source the setup file and then run a Python listener:
```sh
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_py listener
```
![Python Listener Example](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/example%3Alistener.png)

### Set Up Environment in `.bashrc`

Edit the `.bashrc` file and add the following line:

```sh
source /opt/ros/foxy/setup.bash
```
![Edit .bashrc](https://github.com/shathalshehri/ROS-Noetic-Installation/blob/main/write_on_bashrc.png)

---
### References

- [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
- [Ubuntu Downloads](https://ubuntu.com/download/desktop)
- [Ubuntu install of ROS Noetic](https://wiki.ros.org/noetic/Installation/Ubuntu)
- [ROS 2 Installation Guide for Ubuntu](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)
