ROS
=====

ROS - Robot Operating System is an open source robotics platform which can be used as DIY robotics or on an industrial scale. 

Set Locale
----------

     $ sudo apt update && sudo apt install -y locales software-properties-common curl gnupg lsb-release
     $ sudo locale-gen en_US en_US.UTF-8
     $ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
     $ export LANG=en_US.UTF-8
     $ locale

Install
-------

     $ sudo add-apt-repository universe
     $ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
     $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
     # This installs everything. 
     $ sudo apt update && sudo apt install -y ros-humble-desktop-full
     # If you rather not have any gui tools , a minimal install
     $ sudo apt install ros-humble-ros-base
     # If you want to install Dev-tools
     $ sudo apt install ros-dev-tools

Test
----

     $ source /opt/ros/humble/setup.bash
     $ ros2 run demo_nodes_cpp talker
     In another terminal source the setup file and then run a Python listener:
     $ source /opt/ros/humble/setup.bash
     $ ros2 run demo_nodes_py listener
    
Notes
-----

     * You should see the talker saying that it’s Publishing messages and the listener saying I heard those messages. This verifies both the C++ and Python 
       APIs are working properly. 
     * Continue with the tutorials and demos to configure your environment, create your own workspace and packages, and learn ROS 2 core concepts.Using the 
       ROS 1 bridge
     * The ROS 1 bridge can connect topics from ROS 1 to ROS 2 and vice-versa.
     * The default middleware that ROS 2 uses is Cyclone DDS, but the middleware (RMW) can be replaced at runtime.

Optional: Uninstall
-------------------

     $ sudo apt remove ~nros-humble-* && sudo apt autoremove
     $ sudo rm /etc/apt/sources.list.d/ros2.list
     $ sudo apt autoremove && sudo apt autoclean
  
  
References
----------

     https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html

