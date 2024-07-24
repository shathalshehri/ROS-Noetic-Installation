
# ROS Noetic on Ubuntu 20.04.3 Installation Guide

## 1. Installing ROS Noetic on Ubuntu 20.04 LTS

In this section, I will show you how to install ROS on the Ubuntu operating system. I’ve already installed Ubuntu 20.04.3 on a Virtual Machine. If you haven't installed VirtualBox on your operating system yet, you can install it using the references below. You will also need to download the Ubuntu ISO from their website.

1. [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. [Download Ubuntu ISO](https://ubuntu.com/download/desktop)

If you encounter any difficulties with the installation process, I recommend following the steps in a YouTube video. Simply type your operating system and what you want to install on it. If you encounter any errors, copy and paste them into your browser to understand the problem and find a solution.

### What is ROS (Robot Operating System)?

ROS stands for Robot Operating System, which is more like an environment. It has the ability to connect nodes together. By nodes, we mean pieces of software that can be written in C++ or Python. They can handle tasks such as reading a sensor or controlling a servo. These nodes connect together using a publisher/subscribe protocol.

### Installing ROS Noetic on Ubuntu

Follow the steps below and enter the commands in the terminal:

1. **Setup your sources.list**
    ```sh
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
    *(Insert screenshot of the output)*

2. **Add the official ROS keyring**
    ```sh
    sudo apt install curl # if you haven't already installed curl
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
    *(Insert screenshot of the output)*

3. **Update the ROS package index**
    ```sh
    sudo apt update
    ```
    *(Insert screenshot of the output)*

4. **Install the ROS Noetic package**
    In most cases, you will want to install `ros-noetic-desktop-full` for a full ROS experience (Recommended).
    ```sh
    sudo apt install ros-noetic-desktop-full
    ```
    *(Insert screenshot of the output)*

5. **Verify the Noetic installation**
    You must source this script in every bash terminal you use ROS in:
    ```sh
    source /opt/ros/noetic/setup.bash
    ```
    *(Insert screenshot of the output)*

    Then, write `roscore` to make sure that the installation process was successful:
    ```sh
    roscore
    ```
    *(Insert screenshot of the output)*

---

### References

- [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
- [Ubuntu Downloads](https://ubuntu.com/download/desktop)
