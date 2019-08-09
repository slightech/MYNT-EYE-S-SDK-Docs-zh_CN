.. _slam_orb_slam2:

`ORB_SLAM2 <https://github.com/raulmur/ORB_SLAM2>`_ 如何整合
==============================================================


在 MYNT® EYE 上运行 ORB_SLAM2 ，请依照这些步骤：
------------------------------------------------

1. 下载 `MYNT-EYE-S-SDK <https://github.com/slightech/MYNT-EYE-S-SDK.git>`_ 及安装。
2. 按照一般步骤安装 ORB_SLAM2 。
3. 在 MYNT® EYE 上运行例子。

安装依赖
---------

.. code-block:: bash

  sudo apt-get -y install libglew-dev cmake libgoogle-glog-dev
  cd ~
  git clone https://github.com/stevenlovegrove/Pangolin.git
  cd Pangolin
  mkdir build
  cd build
  cmake ..
  cmake --build .
  sudo make install


ROS 下创建双目节点
------------------------

* 添加 ``Examples/ROS/ORB_SLAM2`` 路径到环境变量 ``ROS_PACKAGE_PATH`` 。打开 ``.bashrc`` 文件，在最后添加下面命令行。

.. code-block:: bash

  export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:~/catkin_ws/src/MYNT-EYE-ORB-SLAM2-Sample

* 运行脚本 `build_ros.sh` ：

.. code-block:: bash

  chmod +x build.sh
  ./build.sh
  chmod +x build_ros.sh
  ./build_ros.sh


Stereo_ROS 例子
~~~~~~~~~~~~~~~~

  * 运行 ORB_SLAM2 ``Stereo_ROS`` 例子

1.运行mynteye节点

.. code-block:: bash

  cd [path of mynteye-s-sdk]
  make ros
  source ./wrappers/ros/devel/setup.bash
  roslaunch mynt_eye_ros_wrapper mynteye.launch

2.打开另一个命令行运行ORB_SLAM2

.. code-block:: bash

  rosrun ORB_SLAM2 mynteye_s_stereo ./Vocabulary/ORBvoc.txt ./config/mynteye_s_stereo.yaml false /mynteye/left_rect/image_rect /mynteye/right_rect/image_rect
