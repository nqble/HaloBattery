# 实验性 4K 集成

恢复证据已更新 2026-11-11（太平洋）。D 阶段构建为实验性版本，非正式发布的支持版本。

## 维护者摘要

| 型号 | 证据 | 剩余工作 |
| --- | --- | --- |
| 第一代 XM2w 4k | Mqtteo0 确认电量与官方工具一致、充电显示以及拔除线缆后的恢复情况 | 即使光标移动并执行刷新，电池报告仍可能保持不可用状态；打开官方工具后即可恢复 |
| XM2w 4k v2 | 已收到私有硬件测试结果 | Janlhin 必须批准最终公开措辞 |

该候选项使用 `FF01:0002`、报告 `0xA1`、身份命令 `0x0E` 和电池命令 `0xB4`。非成功有效载荷将被拒绝。尚未添加任何 `0x0F` 探测或经硬件测试的恢复修复。

## 第一代型号硬件证据

**[Mqtteo0](https://github.com/Mqtteo0)** 测试了 `HaloBattery-XM2w4k-Original-StageD-r1-Windows`。其 [11 月 7 日反馈结果](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) 确认，无线百分比与官方工具一致，连接线缆时充电状态会显示，拔除线缆后百分比会恢复。

最初在[移动和等待或刷新](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6742865971)后报告了恢复情况。11 月 10 日，[打开官方工具似乎是必要的](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6764152209)。[最新回复](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6782283052)确认了光标移动，但通过刷新未能恢复。

[配对诊断](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6777323188)显示：

| 打开官方工具前 | 打开后 |
| --- | --- |
| 无电池结果；`device status 0x08; payload not used` | 45% 接收器读取成功；充电状态未知 |
| 接收器 `VID=3367 PID=1970`（包括 `FF01:0002`）仍保留在列表中 | 相同的第一代型号 Stage D r1 构建 |

怀疑存在空闲状态，但尚未得到确认。报告时间戳之间的 34 秒间隔并非所测量的恢复延迟。更早的 75% 快照并非与官方工具进行的同步对比。接收器重新插拔、长期及多设备检查仍未上报。恢复问题并不影响此前进行的电池/充电检查。

## 恢复假设与软件检查

请求失败后，电池通信可能仍处于卡住状态。[Vole 部分 14](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md#14-a-failed-command-wedges-the-device-until-the-next-probe) 描述了通过 `0x0F` 进行恢复的方法，但其实机证据为 **OP1w 4k v2，Linux 上的鼠标固件 1.07 / 接收器固件 1.01**。这仅是一条线索，而非已确认的 XM2w 原因或解决方案。设备状态、应用程序交互以及经过时间仍属其他可能性。

[日志构建](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-logging-r1) 可在不添加设备命令的情况下识别出故障命令。[11 月 11 日的诊断](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6803300510) 显示，在重启 HaloBattery 前后，身份命令 `0x0E` 均返回 `0x08`。打开官方工具后，一次电池请求返回 `0x01`，但该轮询仍未能通过连续样本一致性检查。所显示的 30% 为缓存数据，而非新接收的读数。

这些失败立即返回了；它们并未表明 HID 调用被阻塞。报告的经过时间涵盖了整个读取尝试，而不仅仅是最终请求。

### 本地超时实验

新的 **仅适用于初代型号** 构建会在独立进程中运行每个状态读取操作。如果工作进程超过八秒的等待时间，应用程序会将其终止，并短暂等待清理完成。仍在终止过程中的工作进程会阻止另一个请求。托盘绝不会关闭另一个工作进程正在使用的句柄。设备枚举操作不受此保护机制的保护。

失败的轮询也会记录已验证的电池样本和故障阶段。读取规则和命令序列保持不变；未添加唤醒命令。这可以防止可能发生的阻塞操作，**但无法解决持续出现的返回 `0x08` 的故障**。

验证：29 项专项测试、七项打包后工作进程模拟测试以及一项模拟托盘检查均已通过。目前未声称已完成硬件验证或完整应用套件测试。该构建版本仅限本地使用：**未发布或提交至 VirusTotal**。现有的扫描链接均不包含此版本。中英文说明均已准备就绪；中文版本采用 Index-Translate 翻译后，又进行了技术性和措辞上的修正，尚待母语者审核。

第一代型号构建版本此前也通过了 17 项专项测试、已记录响应的检查、模拟身份检查以及模拟托盘检查。历史 v2 回复和模拟结果并非第一代型号硬件的证据。

### 调查计划

当前假设是：光标输入可恢复，但电池通信仍卡住；打开官方工具似乎能恢复报告。该工具具体修改了什么尚不清楚。目前尚未确认任何修复方案。

1. 审阅超时实验，再商定有针对性的硬件检查。超时保护与持续返回 `0x08` 的故障应分开调查。
2. 通信恢复后，若连续读数一致性检查仍失败，记录每次电量读数。不要根据缓存的百分比推断这些读数。
3. 在考虑受控的 `0x0F` 实验之前，请审查特定型号相关的睡眠效应和请求详情。本计划未实施或批准任何自动探测回退机制。

另一种可选方案是调查接收器在睡眠/唤醒和电池变化时的通知，从而可能避免在睡眠期间发起查询。[Vole 的协议说明](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md)描述了一种独立的 Windows 通知集合 `FF02:0001`；`FF01:0002` 仍然是命令通道。其等效的 XM2w 行为以及与其他软件的共存性尚未经过验证。目前尚未实现任何通知读取器。

验收要求在不使用官方工具的情况下实现多次恢复，同时保持电池/充电行为不变，且不能出现意外唤醒或睡眠延迟。仅一次成功读取是不够的。

## 集成与下一步

上游 [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) 已于 11 月 8 日将社区历史记录合并至 `pre-release`；[PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) 指出了待处理的Endgame 修正。这两个提交均未包含本候选读取程序。在 11 月 10 日检查时，上游未列出 nqble 提交的任何更正 PR。

在将合并后的修正提交到上游 `pre-release` 之前，请调查恢复情况、完成验证，并就私有发现获取批准。问题排查仍位于 [issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48)。暂不承诺合并或发布日期。

## 下载与注明日期的扫描结果

- [第一代 XM2w 4k 阶段 D r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1)
- [XM2w 4k v2 阶段 D r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1)

解压整个 Windows ZIP 文件，并保留其运行时文件夹。其中包含英文/中文说明。标签源存档并非修改后可执行文件的完整快照；软件包包含评审摘录和基础信息。

VirusTotal 上次检查时间为 **11 月 8 日**，本次更新未重新检查：[原始](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior) 2/71 检测项；[v2](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior) 3/71。两者均存在中等匹配度的 Python DLL 侧加载 Sigma 规则，且至少出现一次 `_internal\python312.dll` 加载失败。这两项均无法证明完整应用成功执行，也未确认为误报。计数可能发生变化；请勿据此禁用防护。

## 署名与发布

Mqtteo0 [允许提供一份署名的技术摘要](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302)。他们的公开观察结果与我们的假设以及 Janlhin 的私人结果相互独立。请参阅[署名与证据边界](credits-and-sources.zh-CN.md)。此处未复现任何原始报告或可识别机器身份的信息。
