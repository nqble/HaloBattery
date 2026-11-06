# XM2we — Jordan 的观察

测试者 Jordan（nqble），使用公开预发布构建 e037304。以下为设备持有者的观察，不是普遍兼容性保证。

| 检查 | 观察结果 |
| --- | --- |
| 无线电量 | HaloBattery 与官方工具均显示85% |
| 接入充电线 | 数秒内出现充电指示 |
| 拔掉充电线 | 手动刷新或下一次一分钟轮询后清除充电状态 |
| 接收器重连 | 移动鼠标后恢复识别 |
| 自然休眠/移动 | 测试期间出现休眠指示，移动后恢复正常 |

本次未测量休眠时长，也未验证电压、充电电流、容量或长期精度。接收器仍在时显示充电，并不能证明直连 USB provider 已获验证。本摘要未记录固件和系统版本。

[公开反馈 issue12](https://github.com/ahmedkhursheed23/HaloBattery/issues/12) · [贡献 PR13](https://github.com/ahmedkhursheed23/HaloBattery/pull/13)

此前与 Janlhin 的[配置器 issue1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1)涉及另一应用；不能替代 HaloBattery 托盘验证。
