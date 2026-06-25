# openarmx_integrated_description

[English](./README.md) | 中文

---

![封面](./image/cover.gif)


OpenFlex 集成机器人系统的 URDF 描述，整合底盘、升降台、双臂和头部。

## 概述

本包提供 OpenArmX 集成机器人的统一 URDF/xacro 描述。它将各子系统的描述包组装为一棵完整的运动学树，并包含 ros2_control 硬件接口定义。

## 机器人结构

集成 xacro（`openarmx_integrated_robot.urdf.xacro`）组合了：

1. **底盘** — 4W4S 全向驱动（`swerve_description`）
2. **升降台** — 线性滑台模块（`lift_slide_description`）
3. **双臂** — 左右 7 自由度手臂 + 夹爪（`openarmx_description`）
4. **头部** — 2 自由度俯仰+偏航头部，含可视化网格（`openarmx_head_description`）
5. **ros2_control** — 所有子系统的硬件接口定义

## 运动学链

```
base_link（底盘）
  ├── fl/fr/bl/br_steering_joint → wheel joints（全向驱动）
  └── lift_base_joint（固定）
       └── lift_base_link → lift_joint（移动副） → lift_carriage_link
            ├── left_link0_base → 左臂（7 关节 + 夹爪）
            ├── right_link0_base → 右臂（7 关节 + 夹爪）
            └── head_base_link → head_pitch_joint → head_yaw_joint
```

## 文件

- `urdf/openarmx_integrated_robot.urdf.xacro` — 主集成 xacro
- `urdf/ros2_control/lift_ros2_control.urdf.xacro` — 升降台 ros2_control 定义
- `urdf/ros2_control/lift_fake_hardware.ros2_control.xacro` — 升降台仿真硬件
- `rviz/integrated_robot.rviz` — 完整机器人可视化 RViz 配置
- `rviz/vla_record_light.rviz` — VLA 录制用轻量 RViz 配置
- `launch/display.launch.py` — 独立可视化启动文件

## Xacro 参数

| 参数 | 默认值 | 描述 |
|------|--------|------|
| `use_fake_hardware` | `false` | 使用仿真硬件接口 |
| `left_arm_can_interface` | `can1` | 左臂 CAN 接口 |
| `right_arm_can_interface` | `can0` | 右臂 CAN 接口 |
| `steering_can_interface` | `can5` | 底盘转向 CAN |
| `driving_can_interface` | `can4` | 底盘驱动 CAN |
| `lift_can_interface` | `can3` | 升降台 CAN 接口 |
| `head_can_interface` | `can2` | 头部 CAN 接口 |
| `control_mode` | `mit` | 电机控制模式 |
| `enable_head` | `true` | 包含头部模型和硬件 |

## 使用方法

```bash
# 编译
\n[English](./README.md) | 中文

---
cd ~/openflex_all/openflex_ws
colcon build --packages-select openarmx_integrated_description

# 独立可视化
\n[English](./README.md) | 中文

---
ros2 launch openarmx_integrated_description display.launch.py

# 生成 URDF
\n[English](./README.md) | 中文

---
xacro $(ros2 pkg prefix openarmx_integrated_description)/share/openarmx_integrated_description/urdf/openarmx_integrated_robot.urdf.xacro
```

## 依赖

- `swerve_description`
- `lift_slide_description`
- `openarmx_description`
- `openarmx_head_description`
- `xacro`、`robot_state_publisher`、`joint_state_publisher`、`rviz2`

## 许可证

本作品采用知识共享 署名-非商业性使用-相同方式共享 4.0 国际许可协议 (CC BY-NC-SA 4.0) 进行许可。

版权所有 (c) 2026 成都长数机器人有限公司 (Chengdu Changshu Robot Co., Ltd.)

详情请参阅 [LICENSE_CN.md](LICENSE) 文件或访问：http://creativecommons.org/licenses/by-nc-sa/4.0/

## 致谢

本包是 OpenArmX 机器人平台生态系统的一部分，专为协作机器人领域的研究和工业应用而开发。

---

## 📞 联系我们

### 成都长数机器人有限公司
**Chengdu Changshu Robotics Co., Ltd.**

| 联系方式 | 信息 |
|---------|------|
| 📧 邮箱 | openarmrobot@gmail.com |
| 📱 电话/微信 | +86-17746530375 |
| 🌐 官网 | <https://openarmx.com/> |
| 🌐 文档 | <http://docs.openarmx.com/> |
| 📍 地址 | 天津经济技术开发区西区新业八街11号华诚机械厂 |
| 👤 联系人 | 王先生 |
