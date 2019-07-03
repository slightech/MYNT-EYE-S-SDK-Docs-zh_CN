.. _calibration_tool:

标定工具的使用
==============


介绍
--------

1.1 支持平台
--------

目前标定工具只支持了 Ubuntu 16.04 LTS 上的发布。但有支持官方、ROS多版 OpenCV 依赖。

====================  ====================  ====================
平台                   架构                  不同依赖
====================  ====================  ====================
Ubuntu 16.04 LTS      x64(amd64)            libopencv-dev
Ubuntu 16.04 LTS      x64(amd64)            ros-kinetic-opencv3
====================  ====================  ====================



1.2 工具包说明
--------

Ubuntu 上提供的是 deb/ppa 安装包，名称上会区分架构、依赖和版本。如下：

* mynteye-s-calibrator-opencv-official-1.0.0_amd64.deb
* mynteye-s-calibrator-opencv-ros-kinetic-1.0.0_amd64.deb

其中，

====================  ====================  ============================================================
依赖标识               依赖包名                详细说明
====================  ====================  ============================================================
opencv-official       libopencv-dev          https://packages.ubuntu.com/xenial/libopencv-dev
opencv-ros-kinetic    ros-kinetic-opencv3    http://wiki.ros.org/opencv3
====================  ====================  ============================================================


1.3 deb 工具包获取
--------

====================  ========================================================================
获取方式                获取地址
====================  ========================================================================
百度网盘                https://pan.baidu.com/s/19rW0fPKUlQj6eldZpZFoAA    提取码: a6ps
Google Drive           https://drive.google.com/open?id=1RsV2WEKAsfxbn-Z5nGjk5g3ml1UDEsDc
====================  ========================================================================



安装
--------

2.1 安装准备
--------
* Ubuntu 16.04 LTS 环境，x64 架构
* 标定工具的 deb 包，按需选择 OpenCV 依赖 (PPA安装不需要此步)

2.2 安装 ppa 包
--------

.. code-block:: bash

  $ sudo add-apt-repository ppa:slightech/mynt-eye-s-sdk
  $ sudo apt-get update
  $ sudo apt-get install mynteye-s-calibrator
  $ sudo ln -sf /opt/myntai/mynteye-s-calibrator/mynteye-s-calibrator /usr/local/bin/ mynteye-s-calibrator


2.3 安装 deb 包
--------
sudo dpkg -i 即可安装 deb 包。如下：

.. code-block:: bash

  $ sudo dpkg -i mynteye-s-calibrator-opencv-official-1.0.0_amd64.deb
  ...
  (Reading database ... 359020 files and directories currently installed.)
  Preparing to unpack mynteye-s-calibrator-opencv-official-1.0.0_amd64.deb ...
  Unpacking mynteye-s-calibrator (1.0.0) over (1.0.0) ...
  Setting up mynteye-s-calibrator (1.0.0) ...

如果遇到了依赖包未安装的错误，例如：

.. code-block:: bash

  $ sudo dpkg -i mynteye-s-calibrator-opencv-official-1.0.0_amd64.deb
  Selecting previously unselected package mynteye-s-calibrator.
  (Reading database ... 358987 files and directories currently installed.)
  Preparing to unpack mynteye-s-calibrator-opencv-official-1.0.0_amd64.deb ...
  Unpacking mynteye-s-calibrator (1.0.0) ...
  dpkg: dependency problems prevent configuration of mynteye-s-calibrator:
  mynteye-s-calibrator depends on libatlas-base-dev; however:
  Package libatlas-base-dev is not installed.

  dpkg: error processing package mynteye-s-calibrator (--install):
  dependency problems - leaving unconfigured
  Errors were encountered while processing:
  mynteye-s-calibrator

可以继续执行 sudo apt-get -f install 完成安装，

.. code-block:: bash

  $ sudo apt-get -f install
  Reading package lists... Done
  Building dependency tree
  Reading state information... Done

  Correcting dependencies... Done
  The following additional packages will be installed:
  libatlas-base-dev
  Suggested packages:
  libblas-doc liblapack-doc
  The following NEW packages will be installed:
  libatlas-base-dev
  0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
  1 not fully installed or removed.
  Need to get 3,596 kB of archives.
  After this operation, 30.8 MB of additional disk space will be used.
  Do you want to continue? [Y/n]
  Get:1 http://cn.archive.ubuntu.com/ubuntu xenial/universe amd64 libatlas-base-dev amd64 3.10.2-9 [3,596 kB]
  Fetched 3,596 kB in 3s (1,013 kB/s)
  Selecting previously unselected package libatlas-base-dev.
  (Reading database ... 358993 files and directories currently installed.)
  Preparing to unpack .../libatlas-base-dev_3.10.2-9_amd64.deb ...
  Unpacking libatlas-base-dev (3.10.2-9) ...
  Setting up libatlas-base-dev (3.10.2-9) ...
  update-alternatives: using /usr/lib/atlas-base/atlas/libblas.so to provide /usr/lib/libblas.so (libblas.so) in auto mode
  update-alternatives: using /usr/lib/atlas-base/atlas/liblapack.so to provide /usr/lib/liblapack.so (liblapack.so) in auto mode
  Setting up mynteye-s-calibrator (1.0.0) ...


使用
--------

3.1 使用准备
--------
* MYNT EYE S 相机
* 棋盘格标定板
* 光照均匀的场景

3.2 使用命令
--------

* 安装好标定工具后，在终端可直接运行 mynteye-s-calibrator 命令进行标定。 -h 可见其选项：

.. code-block:: bash

  $ mynteye-s-calibrator -h
  Usage: mynteye-s-calibrator [options]
  help: mynteye-s-calibrator -h
  calibrate: mynteye-s-calibrator -x 11 -y 7 -s 0.036

  Calibrate MYNT EYE S device.

参数:

-h, --help                  显示帮助信息并退出
-x WIDTH, --width=WIDTH     棋盘格宽, 默认: 11
-y HEIGHT, --height=HEIGHT  棋盘格高, 默认: 7
-s METERS, --square=METERS  棋盘格格子边长, 默认: 0.036
-n NUMBER, --number=NUMBER  用于标定的图片张数, 默认: 11
-p PATH, --path=PATH        保存结果的文件夹名, 默认: 相机SN名
* -x -y -s 用于设定标定板的宽、高、格子大小。宽、高分别指棋盘格横纵向的黑白交叉点数。格子大小，单位是 m


3.3 使用步骤
--------

* 首先，连接好 MYNT EYE S 相机。

* 然后，终端里运行 mynteye-s-calibrator <标定板参数> 命令，标定板参数需要根据使用的标定板来设置，参数说明见上

.. image:: ../../images/tools/calibration001.png
   :width: 60%

* 按提示选择相机某个分辨率的 index ，进行此分辨率下的图像标定。

* S1030相机只需要标定752*480分辨率。S2100 相机需要标定2560*800,1280*400两个分辨率。

* 标定时尽量让标定板铺满相机左右目图像，且照顾到四周（畸变最大）。标定工具会自动评估出合格的图像用于标定计算，在终端上会提示已选中了多少张。

参考的采集图像，如下：

.. image:: ../../images/tools/calibration002.png
   :width: 60%

.. image:: ../../images/tools/calibration003.png
   :width: 60%

.. image:: ../../images/tools/calibration004.png
   :width: 60%

.. image:: ../../images/tools/calibration005.png
   :width: 60%

.. image:: ../../images/tools/calibration006.png
   :width: 60%


* 注：p_x, p_y, size, skew 分别表示采集到图像时，标定板于x 轴、y轴、缩放、倾斜的比例。作一点参考用。

* 一旦达到标定需求采集的图像数目后，就会进行标定计算、输出结果。如下：


.. image:: ../../images/tools/calibration007.png
   :width: 60%


* 1.  终端会打印出左右目的标定结果

* 2.  标定结果会写进 SNXXX 目录的文件中

    a)  camera_left.yaml: 左目参数
    b)  camera_right.yaml: 右目参数
    c)  extrinsics.yaml: 双目外参
    d)  img.params.equidistant: 相机参数，可用于 S SDK 写入
    e)  stereo_reprojection_error.yaml: 重投影误差

* 最后，还会询问是否写入相机设备。回车或`y`即表示确认，

.. image:: ../../images/tools/calibration008.png
   :width: 60%

* 写入设备后，将提示“Write to device done”。



3.4 标定结果
--------
标定结果，要求重投影误差最好能达到0.2或更低。如果超过1，需要重新标定。

重投影误差，可见标定完成后的输出“Final reprojection error: 0.201
pixels”，或者见标定结果文件“stereo_reprojection_error.yaml”。
































