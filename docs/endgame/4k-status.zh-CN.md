# 实验性 4K 集成

恢复证据已更新 2026-11-10（太平洋）。D 阶段构建为实验性版本，非正式发布的支持版本。

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

源码审阅和九项针对性模拟测试表明，该候选项在失败后会持续轮询并重新打开句柄，包括缓存图标过期后也是如此。诊断工具无法区分 `0x0E` 处的失败与 `0xB4` 处的失败。另一项仅用于日志记录的提案增加了命令、状态、响应长度和读取耗时；该提案尚未打包成新的可执行文件。

第一代型号构建版本此前也通过了 17 项专项测试、已记录响应的检查、模拟身份检查以及模拟托盘检查。历史 v2 回复和模拟结果并非第一代型号硬件的证据。

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
