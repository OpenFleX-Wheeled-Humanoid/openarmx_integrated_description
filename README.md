# openarmx_integrated_description

English | [中文](./README-CN.md)

---

![Cover](./image/cover.gif)


Integrated URDF description for the OpenFlex robot system combining chassis, lift, dual arms, and head.

## Overview

This package provides the unified URDF/xacro description of the OpenArmX integrated robot. It assembles sub-models from separate description packages into one coherent kinematic tree with ros2_control hardware interface definitions.

## Robot Structure

The integrated xacro (`openarmx_integrated_robot.urdf.xacro`) composes:

1. **Chassis** — 4W4S swerve drive (`swerve_description`)
2. **Lift** — Linear slide module (`lift_slide_description`)
3. **Dual Arms** — Left and right 7-DOF arms + grippers (`openarmx_description`)
4. **Head** — 2-DOF pitch + yaw head with visual meshes (`openarmx_head_description`)
5. **ros2_control** — Hardware interface definitions for all subsystems

## Kinematic Chain

```
base_link (chassis)
  ├── fl/fr/bl/br_steering_joint → wheel joints (swerve)
  └── lift_base_joint (fixed)
       └── lift_base_link → lift_joint (prismatic) → lift_carriage_link
            ├── left_link0_base → left arm (7 joints + gripper)
            ├── right_link0_base → right arm (7 joints + gripper)
            └── head_base_link → head_pitch_joint → head_yaw_joint
```

## Files

- `urdf/openarmx_integrated_robot.urdf.xacro` — Main integrated xacro
- `urdf/ros2_control/lift_ros2_control.urdf.xacro` — Lift ros2_control definition
- `urdf/ros2_control/lift_fake_hardware.ros2_control.xacro` — Lift mock hardware
- `rviz/integrated_robot.rviz` — RViz config for full robot visualization
- `rviz/vla_record_light.rviz` — Lightweight RViz config for VLA recording
- `launch/display.launch.py` — Standalone visualization launch

## Xacro Arguments

| Argument | Default | Description |
|----------|---------|-------------|
| `use_fake_hardware` | `false` | Use mock hardware interfaces |
| `left_arm_can_interface` | `can1` | Left arm CAN interface |
| `right_arm_can_interface` | `can0` | Right arm CAN interface |
| `steering_can_interface` | `can5` | Chassis steering CAN |
| `driving_can_interface` | `can4` | Chassis driving CAN |
| `lift_can_interface` | `can3` | Lift CAN interface |
| `head_can_interface` | `can2` | Head CAN interface |
| `control_mode` | `mit` | Motor control mode |
| `enable_head` | `true` | Include head model and hardware |

## Usage

```bash
# Build

---
cd ~/openflex_all/openflex_ws
colcon build --packages-select openarmx_integrated_description

# Visualize standalone

---
ros2 launch openarmx_integrated_description display.launch.py

# Generate URDF

---
xacro $(ros2 pkg prefix openarmx_integrated_description)/share/openarmx_integrated_description/urdf/openarmx_integrated_robot.urdf.xacro
```

## Dependencies

- `swerve_description`
- `lift_slide_description`
- `openarmx_description`
- `openarmx_head_description`
- `xacro`, `robot_state_publisher`, `joint_state_publisher`, `rviz2`

## License

This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0).

Copyright (c) 2026 Chengdu Changshu Robot Co., Ltd. (成都长数机器人有限公司)

For more details, see the [LICENSE](LICENSE) file or visit: http://creativecommons.org/licenses/by-nc-sa/4.0/

## Acknowledgments

This package is part of the OpenArmX robotic platform ecosystem, developed for research and industrial applications in collaborative robotics.

---

## 📞 Contact Us

### Chengdu Changshu Robot Co., Ltd.

| Contact           | Information                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| 📧 Email          | [openarmrobot@gmail.com](mailto:openarmrobot@gmail.com)                                                      |
| 📱 Phone / WeChat | +86-17746530375                                                                                              |
| 🌐 Website        | [https://openarmx.com/](https://openarmx.com/)                                                               |
| 🌐 Documentation  | [http://docs.openarmx.com/](http://docs.openarmx.com/)                                                               |
| 📍 Address        | Huacheng Machinery Plant, No.11 Xinye 8th Street, West Area, Tianjin Economic-Technological Development Area |
| 👤 Contact Person | Mr. Wang                                                                                                     |
