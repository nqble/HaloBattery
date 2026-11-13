# 致谢与证据边界

- **Janlhin** 负责维护 [Endgame Gear Web Configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator)。[公开问题 #1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1) 记录了他们对 XM2we 协议的调查、修复以及与 nqble 的协作情况。这是一个外部来源，并非 nqble 的代码。
- **[Mqtteo0](https://github.com/Mqtteo0)** 独立测试了第一代 XM2w 4k D 阶段构建版本，并[允许发布一份署名的总结](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302)。署名涵盖其报告的电池、充电和恢复情况观察，不包括协议研究或我们提出的解释。请参阅[当前的证据总结](4k-status.zh-CN.md)。
- **nqble** 执行了 XM2we 所有者测试，并在 GPT 的协助下准备了贡献内容以及实验性集成。AI 生成的更改需要审核和硬件验证。
- **HaloBattery 的上游和社区维护者**提供应用程序和集成框架。
- **Vole 贡献者**提供公开的[协议研究](https://github.com/johanneszab/vole)。此处引用的恢复证据已固定范围，仅适用于 OP1w 硬件，而非 XM2w 验证。

**[Janlhin](https://github.com/Janlhin)** — 对原版 XM2w 4k 和 v2 硬件的调查、官方工具比对、充电/休眠及卡死现象的观察、诊断脚本与源码建议，以及技术摘要评审。

## 发布范围

公开来源已建立链接；私人消息、原始报告、附件以及可识别机器身份的信息均不予复现。原始数据的重新分发须另行获得许可。公开源代码仍受其许可证和相关声明约束；发现摘要不授予任何复用权利。

公共协议背景包括 [Janlhin 的配置器](https://github.com/Janlhin/Endgame_Gear_Web_Configurator)、[mouse-battery-monitor 的 ENDGAME.md（修订版 25871cce）](https://github.com/stuffz/mouse-battery-monitor/blob/25871cce3a8266d8d2bc05b0ca81fbb74b3a38b4/docs/ENDGAME.md) 以及 [Vole 的协议文档](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md)。

ENDGAME.md 独立记录了毫伏字段、5 档百分比刻度、`0x08` 的陈旧缓冲区规则以及有线充电展示。Vole 的 OP1w 发现提供了调查背景；它们未被视作 XM2w 行为的证据。每个项目均保留其自身的署名和许可条款。
