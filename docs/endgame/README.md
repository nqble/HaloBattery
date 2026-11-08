# Endgame Gear battery findings

English | [简体中文](README.zh-CN.md)

Maintained by [nqble](https://github.com/nqble) in this HaloBattery fork.
This is a record of specific tests and implementation work, not an official Endgame Gear resource or a claim that every XM/OP1 model is supported.

| Model | Evidence in this record | Status |
| --- | --- | --- |
| XM2we | nqble's real-device checks in published HaloBattery pre-release e037304 | Battery comparison, charging display, sleep/wake and receiver reconnection observed |
| XM2w 4k | Mqtteo0's public checks in the original Stage D build; local automated checks | Battery comparison and charging/cable-removal checks passed; broader validation pending |
| XM2w 4k v2 | Experimental integration build | Final public wording awaiting contributor review |
| Other XM/OP1 models | No completed HaloBattery hardware results recorded here | Not established by this record |

- [XM2we observations](xm2we.md)
- [4K integration status](4k-status.md)
- [Credits and evidence boundaries](credits-and-sources.md)

A matching percentage at one point does not calibrate battery accuracy. A successful protocol read does not establish tray lifecycle behavior or support across firmware versions. These are battery reporting/compatibility observations, not battery capacity, runtime or health measurements.
