.. _write_img_params:

写入图像标定参数
==================

SDK 提供了写入图像标定参数的工具 ``img_params_writer`` 。

有关如何获取，请阅读 :ref:`get_img_params` 。此参数会用于计算纠正、视差等。

参考运行命令：

.. code-block:: bash

  ./samples/_output/bin/write_img_params samples/config/img.params

  # Windows
  .\samples\_output\bin\write_img_params.bat samples\config\img.params

.. warning::

  请不要随意覆写参数。另外 ``save_all_infos`` 工具可帮你备份参数。

其中， `samples/config/S1030/img.params.pinhole <https://github.com/slightech/MYNT-EYE-S-SDK/blob/master/samples/config/S1030/img.params.pinhole>`_ 是s1030针孔模型参数文件路径。如果你自己标定了参数，可以编辑此文件，然后执行上述命令写入设备。

.. tip::

  S21XX 对应的相机参数在 ``tools/writer/config/S21XX``
  S1030 对应的相机参数在  ``tools/writer/config/S1030``
  其中equidistant表示等距模型，pinhole表示针孔模型

.. tip::

  旧 SDK 提供的标定参数文件 ``SN*.conf`` 也可用此工具写入设备。
