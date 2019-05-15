.. _write_img_params:

写入图像标定参数
==================

SDK 提供了写入图像标定参数的工具 ``img_params_writer`` 。工具详情可见 `tools/README.md <https://github.com/slightech/MYNT-EYE-S-SDK/tree/master/tools>`_ 。

有关如何获取，请阅读 :ref:`get_img_params` 。此参数会用于计算纠正、视差等。

参考运行命令：

.. code-block:: bash

  ./tools/_output/bin/writer/img_params_writer tools/writer/config/S1030/img.params.equidistant

  # Windows
  .\tools\_output\bin\writer\img_params_writer.bat tools\writer\config\S1030\img.params.equidistant

.. warning::

  请不要随意覆写参数。另外 ``save_all_infos`` 工具可帮你备份参数。

其中， `tools/writer/config/S1030/img.params.pinhole <https://github.com/slightech/MYNT-EYE-S-SDK/blob/master/tools/writer/config/S1030/img.params.pinhole>`_ 是s1030针孔模型参数文件路径。如果你自己标定了参数，可以编辑此文件，然后执行上述命令写入设备。

.. tip::

  S2100/S210A 对应的相机参数在 ``tools/writer/config/S210A``
  S1030 对应的相机参数在  ``tools/writer/config/S1030``
  其中equidistant表示等距模型，pinhole表示针孔模型

.. tip::

  旧 SDK 提供的标定参数文件 ``SN*.conf`` 也可用此工具写入设备。
