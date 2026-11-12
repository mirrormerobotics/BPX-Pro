# BPX-Pro Robot Model Assets

English | [简体中文](README.zh-CN.md)

This repository contains open-source robot description assets for the `BPX-Pro`
platform.

It is intended for developers who need model files for mechanical design review,
visualization, simulation setup, USD-based workflows, and integration research.

## Included Assets

- `step/bpxPro.STEP`: mechanical CAD assembly model in STEP AP203 format
- `bpxPro/bpxPro.urdf`: main URDF model entry for the `bpxPro` robot
- `bpxPro/meshes/`: OBJ and MTL mesh assets referenced by the URDF model
- `mjcf/bpxPro.xml`: MuJoCo MJCF model entry
- `mjcf/meshes/`: OBJ mesh assets referenced by the MJCF model
- `usd/bpxPro.usd`: generated USD asset
- `usd/config.yaml`: USD conversion configuration
- `usd/configuration/`: generated USD configuration layers

## Directory Layout

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

## Quick Start

### STEP (CAD)

Open `step/bpxPro.STEP` in a STEP-compatible CAD application to inspect the
mechanical assembly and measure geometry.

The file header records an export from SolidWorks 2020 on 2026-06-11 in STEP
AP203 format. Length units are millimeters.

### URDF

Use `bpxPro/bpxPro.urdf` as the primary entry when loading the robot in
URDF-compatible tools such as RViz, planning pipelines, or custom parsers.

The URDF references meshes from `bpxPro/meshes/` with paths relative to the
URDF file. Keep the `bpxPro/bpxPro.urdf` and `bpxPro/meshes/` layout together
when copying or packaging the asset directory.

### MuJoCo (MJCF)

Use `mjcf/bpxPro.xml` as the entry file for MuJoCo-based simulation and
validation workflows.

The MuJoCo model sets `meshdir="meshes"` and references meshes from the local
`mjcf/meshes/` directory. It includes a free base joint, 12 actuated leg
joints, motor actuators, joint position and velocity sensors, and IMU-related
sensors.

### USD

Use `usd/bpxPro.usd` for USD-compatible workflows. The generated USD layers are
stored under `usd/configuration/`, and `usd/config.yaml` records the conversion
settings used to generate the USD asset from `bpxPro/bpxPro.urdf`.

## Notes

- Asset paths inside the model files are relative to their current directory layout.
- Joint limits, collision geometry, and inertial properties are included in the URDF, MJCF, and USD model files.
- The URDF model contains fixed ankle joints marked with `dont_collapse="true"`.
- Review compatibility and coordinate conventions in your target toolchain before integration.

## License And Usage

This repository is released under the `BSD-3-Clause` license. See `LICENSE`
for the full license text.
