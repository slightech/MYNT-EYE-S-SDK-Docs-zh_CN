.. _get_img_params:

获取图像标定参数
==================

通过 API 的 ``GetIntrinsics()`` ``GetExtrinsics()`` 函数，就可以获取当前打开设备的图像标定参数和相机使用的模型。

.. tip::
  参数模版可以参考 ``tools/writer/config`` 下的参数文件，其中
  S21XX 对应的相机参数在 ``tools/writer/config/S21XX``
  S1030 对应的相机参数在  ``tools/writer/config/S1030``
  equidistant表示等距模型，pinhole表示针孔模型

.. note::
  相机内参Intrinsics: k表示等距畸变系数，mu,mv对应焦距,v,u对应主点坐标。
  相机外参Extrinsics(从右目往左目): rotation表示旋转矩阵， translation表示平移矩阵。
  D、K、R、P 分别为畸变参数，内参矩阵，矫正矩阵，投影矩阵。
  参考链接:  `ros CameraInfo <http://docs.ros.org/melodic/api/sensor_msgs/html/msg/CameraInfo.html>`_

参考代码片段：

.. code-block:: c++

  auto &&api = API::Create(argc, argv);

  LOG(INFO) << "Intrinsics left: {" << *api->GetIntrinsicsBase(Stream::LEFT)
            << "}";
  LOG(INFO) << "Intrinsics right: {" << *api->GetIntrinsicsBase(Stream::RIGHT)
            << "}";
  LOG(INFO) << "Extrinsics right to left: {"
            << api->GetExtrinsics(Stream::RIGHT, Stream::LEFT) << "}";

参考运行结果，于 Linux 上：

.. code-block:: bash

  $ ./samples/_output/bin/tutorials/get_img_params
  I/utils.cc:48 MYNT EYE devices:
  I/utils.cc:51   index: 0, name: MYNT-EYE-S1030, sn: 4B4C192400090712, firmware: 2.4
  I/utils.cc:60 Only one MYNT EYE device, select index: 0
  I/synthetic.cc:59 camera calib model: kannala_brandt
  I/utils.cc:93 MYNT EYE requests:
  I/utils.cc:96   index: 0, request: width: 752, height: 480, format: Format::YUYV, fps: 60
  I/utils.cc:96   index: 1, request: width: 376, height: 240, format: Format::YUYV, fps: 60
  I/utils.cc:107 There are 2 stream requests, select index:
  0
  I/get_img_params.cc:44 Intrinsics left: {equidistant, width: 752, height: 480, k2: 0.00986113697985857, k3: -0.11937208025856659, k4: 0.19092250072175385, k5: -0.10168315832257743, mu: 356.41566867259672335, mv: 356.31078130432149464, u0: 375.76739787805968263, v0: 246.20025492033516912}
  I/get_img_params.cc:45 Intrinsics right: {equidistant, width: 752, height: 480, k2: -0.02246312175999786, k3: 0.01303393297719630, k4: -0.01735983686524734, k5: 0.00675132874903371, mu: 357.96820061652590539, mv: 357.76889287108474491, u0: 397.09281703352422710, v0: 258.93978588846073308}
  I/get_img_params.cc:46 Extrinsics right to left: {rotation: [0.99997489222742053, 0.00041828202737396, -0.00707389248605010, -0.00042920419615213, 0.99999871813992847, -0.00154256353448567, 0.00707323819170721, 0.00154556094848940, 0.99997378992793495], translation: [-120.01607586757218371, 0.34488126401045993, 0.64552185106557303]}
  ROSMsgInfoPair:
  left:
  width: 752, height: 480
  distortion_model: KANNALA_BRANDT
  D: 0.00986114,-0.119372,0.190923,-0.101683,0,
  K: 356.416,0,375.767,0,356.311,246.2,0,0,1,
  R: 0.999919,-0.00246361,-0.0124477,0.00245407,0.999997,-0.000781093,0.0124496,0.000750482,0.999922,
  P: 357.04,0,511.114,0,0,357.04,311.965,0,0,0,1,0,

  right:
  width: 752, height: 480
  distortion_model: KANNALA_BRANDT
  D: -0.0224631,0.0130339,-0.0173598,0.00675133,0,
  K: 357.968,0,397.093,0,357.769,258.94,0,0,1,
  R: 0.999981,-0.00287357,-0.00537853,0.00287782,0.999996,0.000781842,0.00537626,-0.000797306,0.999985,
  P: 357.04,0,511.114,-42851.3,0,357.04,311.965,0,0,0,1,0,


完整代码样例，请见 `get_img_params.cc <https://github.com/slightech/MYNT-EYE-S-SDK/blob/master/samples/get_img_params.cc>`_ 。
