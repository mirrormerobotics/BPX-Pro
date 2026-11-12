# BPX-Pro 机器人模型资源

[English](README.md) | 简体中文

本仓库提供 `BPX-Pro` 平台的开源机器人模型资源。

适用于需要进行机械设计评审、可视化、仿真配置、USD 工作流和集成研究的开发者。

## 包含的资源

- `step/bpxPro.STEP`：STEP AP203 格式的机械 CAD 装配模型
- `bpxPro/bpxPro.urdf`：`bpxPro` 机器人的 URDF 模型主入口
- `bpxPro/meshes/`：URDF 模型引用的 OBJ 和 MTL 网格资源
- `mjcf/bpxPro.xml`：MuJoCo MJCF 模型入口
- `mjcf/meshes/`：MJCF 模型引用的 OBJ 网格资源
- `usd/bpxPro.usd`：生成的 USD 资源
- `usd/config.yaml`：USD 转换配置
- `usd/configuration/`：生成的 USD 配置层

## 目录结构

```text
BPX-Pro/
├── bpxPro/
│   ├── bpxPro.urdf
│   └── meshes/
├── mjcf/
│   ├── meshes/
│   └── bpxPro.xml
├── step/
│   └── bpxPro.STEP
└── usd/
    ├── bpxPro.usd
    ├── config.yaml
    └── configuration/
```

## 快速开始

### STEP（CAD）

使用支持 STEP 格式的 CAD 软件打开 `step/bpxPro.STEP`，可查看机械装配并测量几何尺寸。

文件头记录的导出软件为 SolidWorks 2020，导出日期为 2026-06-11，格式为 STEP AP203，长度单位为毫米。

### URDF

在 RViz、规划工具链或自定义解析器等支持 URDF 的工具中加载机器人时，使用 `bpxPro/bpxPro.urdf` 作为主入口。

URDF 通过相对于自身文件的路径，引用 `bpxPro/meshes/` 中的网格资源。
复制或打包资源目录时，请一并保留 `bpxPro/bpxPro.urdf` 与 `bpxPro/meshes/` 的目录布局。

### MuJoCo（MJCF）

在 MuJoCo 中进行仿真和验证时，使用 `mjcf/bpxPro.xml` 作为入口文件。

MuJoCo 模型设置了 `meshdir="meshes"`，引用本地 `mjcf/meshes/` 目录中的网格资源。
模型包含一个浮动基座关节、12 个驱动腿部关节、电机执行器、关节位置与速度传感器，以及 IMU 相关传感器。

### USD

在支持 USD 的工具中，使用 `usd/bpxPro.usd` 作为入口文件。
生成的 USD 配置层保存在 `usd/configuration/` 中，`usd/config.yaml` 记录了从 `bpxPro/bpxPro.urdf` 生成 USD 资源时使用的转换设置。

## 注意事项

- 模型文件中的资源路径均相对于当前目录布局。
- URDF、MJCF 和 USD 模型文件包含关节限位、碰撞几何和惯性参数。
- URDF 模型包含标记为 `dont_collapse="true"` 的固定踝关节。
- 集成前，请确认目标工具链的兼容性及坐标约定。

## 许可证与使用

本仓库采用 `BSD-3-Clause` 许可证发布，完整条款见 `LICENSE` 文件。
