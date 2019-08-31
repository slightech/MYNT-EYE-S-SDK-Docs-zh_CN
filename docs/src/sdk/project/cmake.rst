.. _cmake:

CMake 如何使用 SDK
==================

本教程将使用 CMake 创建一个项目来使用 SDK 。

   你可以在 ``<sdk>/samples/simple_demo/project_cmake directory`` 目录下找到工程样例。

准备
----

-  Windows: 安装 SDK 的 exe 包
-  Linux: 使用源代码编译和 ``make install``

创建项目
--------

添加 ``CMakeLists.txt`` 和 ``mynteye_demo.cc`` 文件，

.. code-block:: cmake

   cmake_minimum_required(VERSION 3.0)

   project(mynteyed_demo VERSION 1.0.0 LANGUAGES C CXX)

   # flags

   set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -O3")
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O3")

   set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c++11 -march=native")
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -march=native")

   ## mynteye_demo

   add_executable(mynteye_demo mynteye_demo.cc)
   target_link_libraries(mynteye_demo mynteye ${OpenCV_LIBS})

配置项目
--------

增加 ``mynteye`` 和 ``OpenCV`` 到 ``CMakeLists.txt`` ，

.. code-block:: cmake

    # packages

    if(MSVC)
      set(SDK_ROOT "$ENV{MYNTEYES_SDK_ROOT}")
      if(SDK_ROOT)
        message(STATUS "MYNTEYES_SDK_ROOT: ${SDK_ROOT}")
        list(APPEND CMAKE_PREFIX_PATH
          "${SDK_ROOT}/lib/cmake"
          "${SDK_ROOT}/3rdparty/opencv/build"
        )
      else()
        message(FATAL_ERROR "MYNTEYES_SDK_ROOT not found, please install SDK firstly")
      endif()
    endif()

    ## mynteye

    find_package(mynteye REQUIRED)
    message(STATUS "Found mynteye: ${mynteye_VERSION}")

    # When SDK build with OpenCV, we can add WITH_OPENCV macro to enable some
    # features depending on OpenCV, such as ToMat().
    if(mynteye_WITH_OPENCV)
      add_definitions(-DWITH_OPENCV)
    endif()

    ## OpenCV

    # Set where to find OpenCV
    #set(OpenCV_DIR "/usr/share/OpenCV")

    # When SDK build with OpenCV, we must find the same version here.
    find_package(OpenCV REQUIRED)
    message(STATUS "Found OpenCV: ${OpenCV_VERSION}")

将 ``include_directories`` 和 ``target_link_libraries`` 添加到
``mynteye_demo`` 目标，

.. code-block:: cmake

    # targets

    include_directories(
      ${OpenCV_INCLUDE_DIRS}
    )

    ## mynteye_demo

    add_executable(mynteye_demo mynteye_demo.cc)
    target_link_libraries(mynteye_demo mynteye ${OpenCV_LIBS})

使用SDK
-------

可以参考工程样例添加头文件和使用 API 。

Windows
~~~~~~~

可以参考 :ref:`install_windows_exe`, 安装编译工具。

然后打开 “x64 Native Tools Command Prompt for VS 2017”
命令行来编译和运行，

.. code-block:: bat

   mkdir _build
   cd _build

   cmake -G "Visual Studio 15 2017 Win64" ..

   msbuild.exe ALL_BUILD.vcxproj /property:Configuration=Release

   .\Release\mynteye_demo.exe

Linux
~~~~~

打开命令行来编译和运行，

.. code-block:: bash

   mkdir _build
   cd _build/

   cmake ..

   make

   ./mynteye_demo
