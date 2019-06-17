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

安装Docker
----------

.. code-block:: bash

  sudo apt-get update
  sudo apt-get install \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg-agent \
      software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"
  sudo apt-get update
  sudo apt-get install docker-ce docker-ce-cli containerd.io

然后通过 ``sudo usermod -aG docker $YOUR_USER_NAME`` 命令将账号加到 ``docker`` 组。如果遇到 ``Permission denied`` 错误，请登出后再重新登录。



安装 MYNT-EYE-VINS-FUSION-Samples
---------------------------------

.. code-block:: bash

  git clone https://github.com/slightech/MYNT-EYE-VINS-FUSION-Samples.git
  cd MYNT-EYE-VINS-FUSION-Samples/docker
  make build

编译docker推荐16G以上内存，或者内存和虚拟内存加起来大于16G。

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

  cd path/to/MYNT-EYE-VINS-FUSION-Samples/docker
  ./run.sh mynteye-s/mynt_stereo_imu_config.yaml  # Stereo fusion
  # ./run.sh mynteye-s2100/mynt_stereo_config.yaml # Stereo fusion with mynteye-s2100
  # ./run.sh mynteye-s2100/mynt_stereo_imu_config.yaml # Stereo+imu fusion with mynteye-s2100