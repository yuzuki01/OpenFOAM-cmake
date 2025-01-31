# OpenFOAM-cmake

语言: [English](README.md) | [中文](README_zh.md)

适用于 CLion 的 OpenFOAM CMake 配置

* 用于在 CLion 中编译 OpenFOAM 的 CMake 配置
* 使用 icoFoam 来验证安装过程 
* 链接了 OpenFOAM 库和依赖
* 提供了 CMakeLists.txt 模板

## 环境

* gcc-13.2.0
* cmake-3.25.3
* openmpi-5.0.3
* OpenFOAM-6

## 编译

```shell
cmake --build cmake-build-release --target icoFoam -- -j 8
```

## icoFoam

```shell
cd cavity
blockMesh
icoFoam
```
