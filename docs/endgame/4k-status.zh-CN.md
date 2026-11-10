# 实验性 4K 集成状态

恢复状态最近更新：2026-11-10（太平洋）。其他带日期的检查仍保留其注明的日期。

nqble 在 GPT 的协助下，为初代 XM2w 4k 和 v2 准备了便携式的 HaloBattery 测试构建版本。这些是实验性构建版本，并不代表已发布支持。初代机型的电池和充电检查已通过，但在一个已报告的配置上，检测恢复仍不一致且尚未解决。

| 型号 | 下载 | 公开状态 |
| --- | --- | --- |
| 第一代 XM2w 4k | [第一代 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | 电池/充电检查已通过；检测恢复不一致且未解决 |
| XM2w 4k v2 | [V2 阶段 D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | 已收到硬件测试结果；Janlhin 私下提供的硬件测试摘要待最终措辞批准 |

## 第一代 XM2w 4k：独立用户测试

2026-11-07，**[Mqtteo0](https://github.com/Mqtteo0)** 确认测试了本分支提供的 `HaloBattery-XM2w4k-Original-StageD-r1-Windows`。他们的[公开结果](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809)确认：

- 无线连接时的电量百分比与官方 Endgame Gear 软件显示的一致。
- 连接充电线后，会显示充电状态。
- 拔掉线缆后，重新显示电量百分比。

Mqtteo0 最初[报告了检测丢失](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6722818667)。在[11 月 9 日的说明](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6742865971)，他们报告了待机状态，随后在移动、等待或刷新后恢复。在他们的[11 月 10 日的后续反馈](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6764152209)中，前一天移动鼠标即可恢复电量显示，但现在每次似乎都需要打开官方工具。

恢复问题仍未解决。在[11 月 10 日稍后附有恢复前后诊断报告的回复](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6777323188)中，Mqtteo0 怀疑是空闲时间所致，因为他们经常使用游戏手柄，但尚不确定。等待时间、手动刷新失败，以及故障期间光标输入正常等问题仍未得到证实。现有证据不能证明轮询会导致设备进入睡眠状态；接收器重新插拔、长期及多设备检查的结果仍未上报。

恢复前的报告未显示当前电量结果，并记录了 `device status 0x08; payload not used`。接收器仍列为 `VID=3367 PID=1970`，包括 `FF01:0002`。来自同一第一代型号 Stage D r1 构建的恢复后报告通过接收器显示出 45%，充电状态未知。报告时间戳相差 34 秒；这并非从鼠标移动或工具启动测得的恢复延迟。

在候选解析器中，`0x08` 表示非成功状态，其有效负载会被拒绝；这些报告不足以确定其确切原因。因此，失败快照显示的是仍能枚举到接收器，并收到了协议状态响应，而不仅仅是一个缺失的 USB 设备或托盘图标。历史输入触发的轮询条目并不能证明在失败快照发生时 XM 鼠标本身正在移动。

### 相关协议证据：型号范围至关重要

[Vole 部分 14](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md#14-a-failed-command-wedges-the-device-until-the-next-probe) 报告称，由一次成功的 `0x0F` 探测清除了因失败命令导致的通信卡住的状态。其实机证据来自 OP1w 4k v2、鼠标固件 1.07 和接收器固件 1.01（运行于 Linux 系统上）——这并非第一代 XM2w 4k 的验证。

这是一种合理的恢复机制，而非对 Mqtteo0 报告的确定性解释。我们的候选方案仅允许 `0x0E` 和 `0xB4`；尚未添加任何探测回退功能。九项针对性模拟测试均已通过，其中包括一些检查，表明当前的诊断无法区分身份请求失败与电池请求失败。另一项仅用于诊断的提案可在不更改设备请求的情况下，增加命令/状态/长度/时序信息。硬件恢复和新可执行文件均未经过测试。


## 工作假设：尚未证实

在电池通信仍不可用时，常规鼠标输入可能会恢复，打开官方工具可能使该通信恢复。这仅是一种集成假设，而非经所有者确认的观察结果。可能的解释包括读取程序的恢复处理、设备/接收器状态、重新建立通信、应用程序交互，或仅仅是经过的时间更长。目前尚未确定任何具体机制或第一代型号特有的缺陷。

配对诊断现已将故障范围缩小为与仍可枚举到的接收器之间的状态通信失败。其他有用的检查包括：故障期间的光标移动情况、手动刷新是否成功，以及在官方工具关闭时重复执行睡眠/唤醒操作的行为。这些仍为建议的检查项，并非已完成的测试，也不代表请求发送猜测的唤醒命令。此前成功的电池和充电检查仍然有效。

11 月 9 日说明所附的诊断结果确认了第一代 Stage D r1 构建，显示通过接收器成功读到 75% 电量，并记录了在电量读数呈灰色时由输入触发的轮询。该快照并非与官方工具进行的同步 75% 比较。此处未转载任何原始日志或可识别机器身份的信息。

Mqtteo0 [已同意按上述范围总结结果并署名](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302)，用于测试结果页面和修正 PR。这些结果独立于 Janlhin 的测试，且不构成对 Janlhin 私下提供的结果进行发布的授权。

## 自动化检查

第一代型号候选版本通过了 17 项专项自动化测试、打包程序的解析器回放和模拟身份检查以及模拟托盘检查。解析器测试中使用的历史 v2 响应并非第一代型号硬件证据。这些检查不衡量真实设备的准确性或可靠性。

## 上游集成与后续步骤

上游 [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) 已于 2026-11-08 将社区开发历史合并到原项目的 `pre-release` 分支。后续 [PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) 记录了待提交的 Endgame 修正。这两项集成都未包含本分支的修正版 4K 读取程序。

预期的修正 PR 将针对上游 `pre-release`。下一步是调查不一致的检测恢复问题，完成剩余的验证工作，并为私有发现获取最终措辞批准。请在 [社区问题 #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) 中继续排查故障，并在修正 PR 中链接相关证据。暂不承诺合并或发布日期。

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
