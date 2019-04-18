.. _slam_vins_fusion:

`VINS-Fusion <https://github.com/HKUST-Aerial-Robotics/Vins-Fusion>`_ 如何整合
==============================================================================


在 MYNT® EYE 上运行 VINS-Fusion，请依照这些步骤：
--------------------------------------------------

1. 下载 `MYNT-EYE-S-SDK <https://github.com/slightech/MYNT-EYE-S-SDK.git>`_ 及安装 mynt_eye_ros_wrapper。
2. 按照一般步骤安装 VINS-Fusion 。
3. 运行 mynt_eye_ros_wrapper 和 VINS-Fusion 。


快捷安装 ROS Kinetic (若已安装，请忽略)
---------------------------------------

.. code-block:: bash

  cd ~
  wget https://raw.githubusercontent.com/oroca/oroca-ros-pkg/master/ros_install.sh && \
  chmod 755 ./ros_install.sh && bash ./ros_install.sh catkin_ws kinetic

安装Ceres
----------

.. code-block:: bash

  cd ~
  git clone https://ceres-solver.googlesource.com/ceres-solver
  sudo apt-get -y install cmake libgoogle-glog-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev
  sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
  sudo apt-get update && sudo apt-get install libsuitesparse-dev
  mkdir ceres-bin
  cd ceres-bin
  cmake ../ceres-solver
  make -j3
  sudo make install


安装 MYNT-EYE-VINS-FUSION-Samples
---------------------------------

.. code-block:: bash

  mkdir -p ~/catkin_ws/src
  cd ~/catkin_ws/src
  git clone https://github.com/slightech/MYNT-EYE-VINS-FUSION-Samples.git
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
  roslaunch mynt_eye_ros_wrapper vins_fusion.launch

2.打开另一个命令行运行vins

.. code-block:: bash

  cd ~/catkin_ws/src
  source ./devel/setup.bash
  roslaunch vins mynteye-s-stereo.launch  # Stereo fusion / Stereo+imu fusion
  # roslaunch vins mynteye-s-mono-imu.launch  # mono+imu fusion
  # roslaunch vins mynteye-s2100-mono-imu.launch  # mono+imu fusion with mynteye-s2100
  # roslaunch vins mynteye-s2100-stereo.launch  # Stereo fusion / Stereo+imu fusion with mynteye-s2100
