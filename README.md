# OpenFOAM-cmake

Language: [English](README.md) | [中文](README_zh.md)

OpenFOAM CMake Configuration for CLion.

* CMake configuration for building OpenFOAM in CLion
* Example using icoFoam to demonstrate the setup process
* Setup instructions for linking OpenFOAM libraries and dependencies
* Sample CMakeLists.txt templates for easy project initialization

## Environment

* gcc-13.2.0
* cmake-3.25.3
* openmpi-5.0.3
* OpenFOAM-6

## Compile

```shell
cmake --build cmake-build-release --target icoFoam -- -j 8
```

## icoFoam

```shell
cd cavity
blockMesh
icoFoam
```
