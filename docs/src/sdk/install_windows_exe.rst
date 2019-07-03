.. _install_windows_exe:

Windows EXE 安装
=====================

.. only:: html

  +-----------------+
  | Windows 10      |
  +=================+
  | |build_passing| |
  +-----------------+

  .. |build_passing| image:: https://img.shields.io/badge/build-passing-brightgreen.svg?style=flat

.. only:: latex

  +-----------------+
  | Windows 10      |
  +=================+
  | ✓               |
  +-----------------+

下载并安装 SDK
---------------

.. tip::

  下载地址： mynteye-s-x.x.x-win-x64-opencv-3.4.3.exe `Google Drive <https://drive.google.com/open?id=1PYC_5Mh2pzLFVXkYlkllEzPnr50EbKht>`_ `百度网盘(提取码:rj4k) <https://pan.baidu.com/s/1yCKjvivB2gsqTV8xyY7DQg>`_ 。

安装完 SDK 的 exe 安装包后，桌面会生成 SDK 根目录的快捷方式。

.. tip::

  <SDK_ROOT_DIR>是指exe包安装路径

进入 ``<SDK_ROOT_DIR>\bin\samples\tutorials`` 目录，双击 ``get_stereo.exe`` 运行，即可看到双目实时画面。

如果样例没有运行成功，请先检查一下系统变量PATH中是否成功添加了 ``<SDK_ROOT_DIR>\3rdparty\opencv\build``, ``<SDK_ROOT_DIR>\bin`` 路径，如果没有需要手动添加一下。

生成样例工程
------------

首先，安装好 `Visual Studio 2017 <https://visualstudio.microsoft.com/>`_ 和 `CMake <https://cmake.org/>`_ 。

接着，进入 ``<SDK_ROOT_DIR>\samples`` 目录， 双击 ``generate.bat`` 即可生成样例工程。

.. tip::

  运行样例需要先右键样例，设为启动项目，然后使用Release x64运行

p.s. 样例教程，可见 `SDK <https://slightech.github.io/MYNT-EYE-S-SDK/>`_ 主页给出的 Guide 文档。

如何于 Visual Studio 2017 下使用 SDK
------------------------------------

进入 ``<SDK_ROOT_DIR>\projects\vs2017`` ，见 ``README.md`` 说明。
