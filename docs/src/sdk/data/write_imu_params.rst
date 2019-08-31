.. _write_imu_params:

写入 IMU 标定参数
===================

SDK 提供了写入 IMU 标定参数的工具 ``imu_params_writer`` 。

有关如何获取，请阅读 :ref:`get_imu_params` 。

参考运行命令：

.. code-block:: bash

  ./samples/_output/bin/write_imu_params samples/config/imu.params

  # Windows
  .\samples\_output\bin\write_imu_params.bat samples\config\imu.params

其中， `samples/config/imu.params <https://github.com/slightech/MYNT-EYE-S-SDK/blob/master/samples/config>`_ 是参数文件夹路径。如果你自己标定了参数，可以编辑此文件，然后执行上述命令写入设备。

.. warning::

  请不要随意覆写参数。另外 ``save_all_infos`` 工具可帮你备份参数。