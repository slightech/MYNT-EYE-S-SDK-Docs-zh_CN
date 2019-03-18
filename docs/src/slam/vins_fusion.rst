.. _slam_vins_fusion:

`VINS-Fusion <https://github.com/HKUST-Aerial-Robotics/Vins-Fusion>`_ 如何整合
==============================================================================


在 MYNT® EYE 上运行 VINS-Fusion，请依照这些步骤：
--------------------------------------------------

1. 下载 `MYNT-EYE-S-SDK <https://github.com/slightech/MYNT-EYE-S-SDK.git>`_ 及安装 mynt_eye_ros_wrapper。
2. 按照一般步骤安装 VINS-Fusion 。
3. 运行 mynt_eye_ros_wrapper 和 VINS-Fusion 。


准备步骤
--------

1. 安装 Ubuntu 64位 16.04/18.04. ROS Kinetic/Melodic(如果已经安装ROS可以跳过). `ROS安装步骤 <http://wiki.ros.org/ROS/Installation>`_
2. 安装 `Ceres <http://ceres-solver.org/installation.html>`_


安装 MYNT-EYE-VINS-FUSION-Samples
---------------------------------

.. code-block:: bash

  mkdir -p ~/catkin_ws/src
  cd ~/catkin_ws/src
  git clone -b mynteye https://github.com/slightech/MYNT-EYE-VINS-FUSION-Samples.git
  cd ..
  catkin_make
  source ~/catkin_ws/devel/setup.bash

(如果安装失败，请尝试换一台系统干净的电脑或者重新安装系统与ROS)

在 MYNT® EYE 上运行 VINS-FUSION
-------------------------------

1.运行mynteye节点

.. code-block:: bash

  cd (local path of MYNT-EYE-S-SDK)
  source ./wrappers/ros/devel/setup.bash
  roslaunch mynt_eye_ros_wrapper mynteye.launch

2.打开另一个命令行运行vins

.. code-block:: bash

  cd ~/catkin_ws
  roslaunch vins mynteye-s-mono-imu.launch  # mono+imu fusion
  # roslaunch vins mynteye-s-stereo.launch  # Stereo fusion / Stereo+imu fusion
  # roslaunch vins mynteye-avarta-mono-imu.launch  # mono+imu fusion with mynteye-avarta
  # roslaunch vins mynteye-avarta-stereo.launch  # Stereo fusion / Stereo+imu fusion with mynteye-avarta
