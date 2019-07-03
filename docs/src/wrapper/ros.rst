.. _wrapper_ros:

ROS 如何使用
==============

按照 :ref:`sdk_install_ros_wrapper` ，编译再运行节点。

.. tip::

  使用下面命令前需要先在另一个命令行窗口运行ROS节点

``rostopic list`` 可以列出发布的节点：

.. code-block:: bash

  $ rostopic list
  /mynteye/depth/image_raw
  /mynteye/disparity/image_norm
  /mynteye/disparity/image_raw
  /mynteye/imu/data_raw
  /mynteye/left/camera_info
  /mynteye/left/image_raw
  /mynteye/left/image_rect
  /mynteye/points/data_raw
  /mynteye/right/camera_info
  /mynteye/right/image_raw
  /mynteye/right/image_rect
  /mynteye/temp/data_raw
  ...

``rostopic hz <topic>`` 可以检查是否有数据：

.. code-block:: bash

  $ rostopic hz /mynteye/imu/data_raw
  subscribed to [/mynteye/imu/data_raw]
  average rate: 505.953
    min: 0.000s max: 0.018s std dev: 0.00324s window: 478
  average rate: 500.901
    min: 0.000s max: 0.018s std dev: 0.00327s window: 975
  average rate: 500.375
    min: 0.000s max: 0.019s std dev: 0.00329s window: 1468
  ...

``rostopic echo <topic>`` 可以打印发布数据等。了解更多，请阅读 `rostopic <http://wiki.ros.org/rostopic>`_ 。

ROS 封装的文件结构，如下所示：

.. code-block:: none

  <sdk>/wrappers/ros/
  ├─src/
  │  └─mynt_eye_ros_wrapper/
  │     ├─config/
  │     │  ├─device/
  │     │     ├─standard.yaml   # S1030
  │     │     └─standard2.yaml  # S2100/S210A
  │     │  ├─laserscan/
  │     │  ├─process/
  │     │  └─...
  │     ├─launch/
  │     │  ├─display.launch
  │     │  └─mynteye.launch
  │     │  └─...
  │     ├─msg/
  │     ├─rviz/
  │     ├─src/
  │     │  ├─wrapper_node.cc
  │     │  └─wrapper_nodelet.cc
  │     ├─CMakeLists.txt
  │     ├─nodelet_plugins.xml
  │     └─package.xml
  └─README.md

其中 ``mynteye.launch`` 里，可以配置发布的 topics 与 frame_ids 、决定启用哪些数据, ``standard.yaml`` (standard2.yaml为S2100/S210A的配置文件) 中可以设定控制选项等。其中，``gravity`` 请配置成当地重力加速度。

standard.yaml/standard2.yaml:

.. code-block:: xml

  # s2100/s210a 修改分辨率/帧率参数
  standard2/request_index: 2

  # s1030 修改帧率/imu频率等
  # standard/frame_rate range: {10,15,20,25,30,35,40,45,50,55,60}
  standard/frame_rate: -1
  # standard/frame_rate: 25

  # standard/imu_frequency range: {100,200,250,333,500}
  standard/imu_frequency: -1
  # standard/imu_frequency: 200

  # s2100 修改曝光时间等
  # standard2/brightness range: [0,240]
  standard2/brightness: -1
  # standard2/brightness: 120
  ...

  # s210a 修改曝光时间等
  # standard210a/brightness range: [0,240]
  standard210a/brightness: -1
  # standard210a/brightness: 120
  ...

mynteye.launch:

.. code-block:: xml

  <arg name="gravity" default="9.8" />

如果想要打印调试信息，请编辑 ``wrapper_node.cc`` ，修改 ``Info`` 为 ``Debug`` 即可：

.. code-block:: c++

  ros::console::set_logger_level(
      ROSCONSOLE_DEFAULT_NAME, ros::console::levels::Info);
