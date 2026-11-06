# XM2we — nqble 的观察记录

由 nqble 测试，使用的已发布 HaloBattery 预发布版本标识为 e037304。以下为设备持有者的观察摘要，不代表普遍兼容性保证。

| 检查项 | 观测结果 |
| --- | --- |
| 无线电量百分比 | HaloBattery 和官方工具均显示85% |
| 接入充电线 | 数秒内出现充电状态指示 |
| 拔除线缆 | 充电状态指示会保留至手动刷新或下一次轮询（间隔约一分钟） |
| 接收器重新连接 | 移动鼠标后恢复识别 |
| 自然休眠/移动 | 测试期间出现休眠指示；移动鼠标后恢复正常指示 |

本次测试未测量休眠时长。未确定确切的电压、充电电流、电池容量和长期精度。接收器仍连接时出现充电指示，并不能证明直连 USB 读取功能已获验证。固件和操作系统版本未记录在此摘要中。

公开跟进：[HaloBattery 问题12](https://github.com/ahmedkhursheed23/HaloBattery/issues/12)。
贡献：[PR13](https://github.com/ahmedkhursheed23/HaloBattery/pull/13)。

早期与 Janlhin 进行的配置器相关工作涉及不同的应用和独立的测试：[公开问题1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1)。这些结果不应计入 HaloBattery 托盘验证。
