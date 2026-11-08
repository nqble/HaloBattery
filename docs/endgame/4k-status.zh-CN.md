# 实验性 4K 集成状态

nqble 在 GPT 的协助下，准备了针对特定型号的便携 HaloBattery 测试构建版本。这些发布版本属于实验性质；它们的存在并不代表所有相关型号均已获支持。

| 型号 | 下载 | 公开状态 |
| --- | --- | --- |
| 第一代 XM2w 4k | [第一代 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | 独立用户的电量和充电检查已通过；更广泛的验证待完成 |
| XM2w 4k v2 | [V2 阶段 D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | 已收到硬件测试结果；最终公开措辞待贡献者审核 |

## 第一代 XM2w 4k：独立用户测试

2026-11-07，**[Mqtteo0](https://github.com/Mqtteo0)** 确认测试了本分支提供的 `HaloBattery-XM2w4k-Original-StageD-r1-Windows`。他们的[公开结果](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809)确认：

- 无线连接时的电量百分比与官方 Endgame Gear 软件显示的一致。
- 连接充电线后，会显示充电状态。
- 拔掉线缆后，重新显示电量百分比。

以上是用户在一套第一代型号设备上的测试反馈。评论中未说明测得的百分比、固件版本或 Windows 版本。该评论也未报告睡眠、接收器重新连接、长期可靠性或多设备行为。此处未转载任何原始日志。

Mqtteo0 [已同意按上述范围总结结果并署名](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302)，用于测试结果页面和修正 PR。这些结果独立于 Janlhin 的测试，且不构成对 Janlhin 私下提供的结果进行发布的授权。

## 本地检查和后续步骤

第一代型号候选版本通过了 17 项专项自动化测试、打包程序的解析器回放和模拟身份检查以及模拟托盘检查。解析器测试中使用的历史 v2 响应并非第一代型号硬件证据。这些检查不衡量真实设备的准确性或可靠性。

第一代型号是本轮测试计划中的最后一个型号。剩余测试和最终措辞审核完成后，nqble 计划提交一份综合修正 PR。上游 [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) 提议将社区开发成果合并回原项目仓库。计划在该集成合并后向上游 `pre-release` 提交；若届时过渡仍未完成，则先与维护者协调提交位置。不保证任何合并或发布日期。第一代软件包和 v2 包是独立的；无需重复进行 v2 测试。

每个 ZIP 文件都包含应用运行时以及英文/中文说明。请下载 Windows ZIP 文件，将其完整解压并保留运行时文件夹。仅凭 GitHub 标签/源码存档并不能构成修改后测试可执行文件的完整源码快照；相关源码节选和基础信息均包含在软件包中。

## 可执行文件扫描

[原始可执行文件报告](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior)：上次审查时间 2026-11-05 太平洋时间，4/68 个引擎报出检测结果，其中包括 Microsoft。沙箱摘要未列出恶意软件检测或释放文件，但不能据此确认应用已配合完整运行库成功启动。尚不能确认这些检测属于误报。

[V2 可执行文件报告](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior)：上次审查于 2026-11-05 太平洋时间，检出 3/71 项。相同的完整运行时执行限制同样适用。计数可能会发生变化；请参阅每份具体报告。这两份报告均不构成安全许可，也不构成禁用防护的理由。

## 来源与发布边界

公开协议上下文：[Janlhin 配置器](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) 和 [Vole](https://github.com/johanneszab/vole)。其公开项目贡献与 nqble 的集成工作分别署名。不得混淆协议族与硬件验证范围。

以私密方式提供的设备特定发现，在获得许可前将不予披露。此处不会发布任何私密消息、报告、日志或可识别设备身份的信息。如需署名技术摘要并重新分发原始证据，须另行达成协议。收到报告并不意味着获准发布其内容。
