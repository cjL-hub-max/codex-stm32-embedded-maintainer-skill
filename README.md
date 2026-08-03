# STM32 FreeRTOS Simple Maintainer Skill

一个面向 Codex 的 STM32CubeMX、STM32CubeIDE 与 FreeRTOS 工程维护 Skill。

它的目标不是把嵌入式工程改造成复杂的软件架构，而是让工程继续保持接近传统：

```text
main.c + 一组清楚的 .c/.h 模块
```

FreeRTOS 只负责调度。主业务流程集中、硬件配置有依据、可移植模块受到保护，最终代码应方便原作者和其他嵌入式工程师继续维护。

> 本项目是社区维护的非官方 Skill，不隶属于 OpenAI、STMicroelectronics 或 FreeRTOS。

## 适用场景

- 检查或整理 STM32 FreeRTOS 工程架构。
- 修复 AI 持续修改后出现的业务分散、宏过多、函数碎片化和命名过长。
- 在不破坏外设驱动、协议或算法模块的前提下增加功能。
- 接手同事工程并输出清楚的项目规划、实施计划、验收结果和交付记录。
- 在修改电机、DMA、定时器或中断前核对完整硬件链路。

## 核心原则

- 采用“一个主业务任务 + 少量必要独立任务”。
- `freertos.c` 只保留 RTOS 资源、任务创建和简洁任务壳。
- 主业务文件像传统 `main.c` 的 `while (1)` 一样顺序展示流程。
- 可移植外设、协议、算法和通用功能 `.c/.h` 默认作为保护模块。
- 所有硬件配置必须从当前工程、`.ioc`、原理图或明确资料核对，禁止猜测。
- 业务变量使用简单英文小写，最多一个下划线。
- 慎用宏，避免一排短小包装函数，也避免职责混杂的超长普通函数。
- 所有变量、宏、结构体成员、枚举值和函数必须有用途注释。
- 只保留一个统一串口日志入口，避免日志刷屏。
- 尽量一次完成读取、规划、修改、构建、验收和交付，减少用户反复介入。

## 仓库结构

```text
.
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── acceptance-checklist.md
    └── final-report-template.md
```

## 安装

将仓库克隆或复制到 Codex 的 Skill 目录：

```bash
git clone https://github.com/cjL-hub-max/codex-stm32-embedded-maintainer-skill.git \
  ~/.codex/skills/stm32-freertos-simple-maintainer
```

Windows PowerShell 示例：

```powershell
git clone https://github.com/cjL-hub-max/codex-stm32-embedded-maintainer-skill.git `
  "$HOME\.codex\skills\stm32-freertos-simple-maintainer"
```

重新启动 Codex 后使用该 Skill。

## 使用示例

```text
使用 $stm32-freertos-simple-maintainer 检查并整理当前 STM32 FreeRTOS 工程。
保持可移植外设和功能模块不变，先从工程确认硬件接口，再一次性完成修改、构建检查、项目规划、实施结果、验收结果和测试步骤。
```

```text
使用 $stm32-freertos-simple-maintainer 为当前工程增加三种追踪模式：
1 纯雷达，2 视觉加热成像，3 融合追踪。
只使用一个模式变量，不新增大量宏和短函数，不猜测硬件配置。
```

## 设计边界

该 Skill 不替代：

- 数据手册、参考手册和原理图核对。
- CubeMX 外设配置审查。
- 实机电气安全与机械限位验证。
- 编译器、链接器和硬件在环测试。

当资料无法确定关键引脚、有效电平、方向、协议、单位或安全参数时，Skill 应停止猜测，并集中提出阻塞问题。

## 贡献

欢迎提交 Issue 或 Pull Request，重点改进：

- 不同 STM32 系列和 CubeIDE 工程的适配经验。
- FreeRTOS 任务、队列、DMA 和中断检查规则。
- 更简洁、可移交的嵌入式工程维护实践。
- 可复现的验收清单和工程案例。

提交改动时，请保持本项目的核心方向：**简单、可读、硬件有依据、最小改动、诚实验证。**

## 许可证

本项目使用 [MIT License](LICENSE)。
