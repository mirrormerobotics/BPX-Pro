# BPX-Pro Robot Model Assets

This repository contains open-source robot description assets for the `BPX-Pro`
platform.

It is intended for developers who need model files for visualization, simulation
setup, USD-based workflows, and integration research.

## Included Assets

- `bpxPro/bpxPro.urdf`: main URDF model entry for the `bpxPro` robot
- `bpxPro/meshes/`: OBJ and MTL mesh assets referenced by the URDF model
- `mujoco/bpxPro.xml`: MuJoCo model entry
- `mujoco/meshes/`: OBJ mesh assets referenced by the MuJoCo model
- `usd/bpxPro.usd`: generated USD asset
- `usd/config.yaml`: USD conversion configuration
- `usd/configuration/`: generated USD configuration layers

## Directory Layout

```text
BPX-Pro/
├── bpxPro/
│   ├── bpxPro.urdf
│   └── meshes/
├── mujoco/
│   ├── meshes/
│   └── bpxPro.xml
└── usd/
    ├── bpxPro.usd
    ├── config.yaml
    └── configuration/
```

## Quick Start

### URDF

Use `bpxPro/bpxPro.urdf` as the primary entry when loading the robot in
URDF-compatible tools such as RViz, planning pipelines, or custom parsers.

The URDF references meshes from `bpxPro/meshes/` with paths relative to the
URDF file. Keep the `bpxPro/bpxPro.urdf` and `bpxPro/meshes/` layout together
when copying or packaging the asset directory.

### MuJoCo

Use `mujoco/bpxPro.xml` as the entry file for MuJoCo-based simulation and
validation workflows.

The MuJoCo model sets `meshdir="meshes"` and references meshes from the local
`mujoco/meshes/` directory. It includes a free base joint, 12 actuated leg
joints, motor actuators, joint position and velocity sensors, and IMU-related
sensors.

### USD

Use `usd/bpxPro.usd` for USD-compatible workflows. The generated USD layers are
stored under `usd/configuration/`, and `usd/config.yaml` records the conversion
settings used to generate the USD asset from `bpxPro/bpxPro.urdf`.

## Notes

- Asset paths inside the model files are relative to their current directory layout.
- Joint limits, collision geometry, and inertial properties are already included in the published model files.
- The URDF model contains fixed ankle joints marked with `dont_collapse="true"`.
- Review compatibility and coordinate conventions in your target toolchain before integration.

## License And Usage

This repository is released under the `BSD-3-Clause` license. See `LICENSE`
for the full license text.
