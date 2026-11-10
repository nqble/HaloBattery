# 实验性 4K 集成状态

事实核查日期：2026-11-09（太平洋时间）。

nqble 使用 GPT 辅助为第一代 XM2w 4k 和 v2 准备了便携测试版本。这些实验版本不代表正式发布的型号支持。第一代型号用户已澄清：待机后移动鼠标，再等待轮询或手动刷新即可恢复电量显示。

| 型号 | 下载 | 公开状态 |
| --- | --- | --- |
| 第一代 XM2w 4k | [第一代 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | 电量和充电检查已通过；已报告待机后恢复，耗时未测量 |
| XM2w 4k v2 | [V2 阶段 D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | 已收到硬件测试结果；Janlhin 私下提供的硬件测试摘要待最终措辞批准 |

## 第一代 XM2w 4k：独立用户测试

2026-11-07，**[Mqtteo0](https://github.com/Mqtteo0)** 确认测试了本分支提供的 `HaloBattery-XM2w4k-Original-StageD-r1-Windows`。他们的[公开结果](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809)确认：

- 无线连接时的电量百分比与官方 Endgame Gear 软件显示的一致。
- 连接充电线后，会显示充电状态。
- 拔掉线缆后，重新显示电量百分比。

Mqtteo0 最初[报告了检测丢失问题](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6722818667)，而当时认为打开再关闭官方软件才能恢复识别。在[2026-11-09 的澄清](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6742865971)中，设备持有者指出待机状态是触发原因：移动鼠标后，等待或刷新 HaloBattery 即可恢复百分比，无需使用官方软件。

这与“待机”后执行“轮询恢复”的流程一致。这并未证明是轮询导致了鼠标进入睡眠状态。恢复延迟尚未测量，设备设备持有者也未报告接收器重插、长期或跨多设备的检查结果。

与该说明相关的诊断结果确认了第一代 Stage D r1 构建，显示通过接收器成功读到 75% 电量，并记录了在电量读数呈灰色时由输入触发的轮询。该快照并非与官方工具进行的同步 75% 比较。此处未转载任何原始日志或可识别机器身份的信息。

Mqtteo0 [已同意按上述范围总结结果并署名](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302)，用于测试结果页面和修正 PR。这些结果独立于 Janlhin 的测试，且不构成对 Janlhin 私下提供的结果进行发布的授权。

## 自动化检查

第一代型号候选版本通过了 17 项专项自动化测试、打包程序的解析器回放和模拟身份检查以及模拟托盘检查。解析器测试中使用的历史 v2 响应并非第一代型号硬件证据。这些检查不衡量真实设备的准确性或可靠性。

## 上游集成与后续步骤

上游 [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) 已于 2026-11-08 将社区开发历史合并到原项目的 `pre-release` 分支。后续 [PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) 记录了待提交的 Endgame 修正。这两项集成都未包含本分支的修正版 4K 读取程序。

修正 PR 计划提交到上游 `pre-release`。下一步是测量待机后的恢复时间、完成剩余验证，并取得私下提供的测试结果的最终公开措辞许可。继续在[社区 issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48)排查，并在修正 PR 中链接相关证据。不承诺合并或发布日期。

## 使用测试下载包

每个 ZIP 文件都包含应用运行时以及英文/中文说明。请下载 Windows ZIP 文件，将其完整解压并保留运行时文件夹。仅凭 GitHub 标签/源码存档并不能构成修改后测试可执行文件的完整源码快照；相关源码节选和基础信息均包含在软件包中。

## 可执行文件扫描

VirusTotal 报告上次核查于 2026-11-08（太平洋时间）：

- [原始可执行文件](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior)：2/71 个引擎检出；Microsoft 显示 Undetected。
- [V2 可执行文件](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior)：3/71 个引擎检出。

两份行为报告均显示存在一次中等风险的 Sigma 匹配项“潜在的 Python DLL 侧加载”，且活动摘要中未检测到恶意软件或已释放的文件。每份报告中至少有一次运行明确未能加载 `_internal\python312.dll`；这些运行并未启动完整应用程序。报告并未证明完整的便携包能够安全运行，也未确认是否存在误报。计数可能会发生变化；任何一份报告都不能作为安全许可，也不能成为禁用防护的理由。

## 来源与发布边界

本记录已收录公开结果，包括 nqble 的 XM2we 测试和 Mqtteo0 的第一代 XM2w 4k 观察。Janlhin 私下提供的硬件测试结果，将在 Janlhin 批准最终公开措辞后补充。这项审核要求不影响已经公开或另获发布许可的结果。

公开协议上下文：[Janlhin 配置器](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) 和 [Vole](https://github.com/johanneszab/vole)。其公开项目贡献与 nqble 的集成工作分别署名。不得混淆协议族与硬件验证范围。

以私密方式提供的设备特定发现，在获得许可前将不予披露。此处不会发布任何私密消息、报告、日志或可识别设备身份的信息。如需署名技术摘要并重新分发原始证据，须另行达成协议。收到报告并不意味着获准发布其内容。
