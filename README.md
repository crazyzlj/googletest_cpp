# C++ UnitTest demo based on Googletest

[![Build Status](https://travis-ci.org/crazyzlj/googletest_cpp.svg?branch=master)](https://travis-ci.org/crazyzlj/googletest_cpp)  [![Build status](https://ci.appveyor.com/api/projects/status/38joe0ke192ecj5i?svg=true)](https://ci.appveyor.com/project/crazyzlj/googletest-cpp)

参考：
+ https://github.com/ShawInnes/cpp-unittesting
+ https://github.com/Crascit/DownloadProject
+ https://crascit.com/2015/07/25/cmake-gtest/
+ https://github.com/google/googletest

## 基本应用

## macOS / Linux
```shell
cd googletest_cpp
mkdir build
cd build
cmake ..
make
bin/unittest_demo_test
```
## Windows
打开VS2013开发人员命令提示：
```shell
cd googletest_cpp
mkdir build
cd build
cmake -G "Visual Studio 12 Win64" ..
msbuild unittest_demo.sln /p:Configuration=Release
Release\unittest_demo_test
同理Debug模式后两行代码为
msbuild unittest_demo.sln /p:Configuration=Debug
Debug\unittest_demo_test
```
即可看到单元测试结果：

![单元测试结果](http://i.imgur.com/kYTs5wt.jpg)