# Endgame Gear battery findings

English | [简体中文](README.zh-CN.md)

Maintained by [nqble](https://github.com/nqble) in this HaloBattery fork.
This is a record of specific tests and implementation work, not an official Endgame Gear resource or a claim that every XM/OP1 model is supported.

## How to read this record

Start with the model table below, then open the linked model page for the tested build, observations and limitations. Model names are distinct: XM2we, original XM2w 4k and XM2w 4k v2 are not interchangeable. A result for one model does not establish support for another.

An owner observation describes what happened on a real device. An automated or simulated check tests software behavior without proving it works on that device. A release status says where the code has been merged or published; passing a test alone does not change that status.

Stage D is the name of this collaboration's portable HaloBattery application test, not a HaloBattery release version or a certification. Original-model and v2 Stage D downloads are separate builds.

## Model status

Public results are documented here, including nqble's XM2we checks and Mqtteo0's original XM2w 4k observations. Janlhin's privately supplied hardware findings will be added after Janlhin approves the final wording. This review requirement does not hold up publication of independently public or separately approved results.

| Model | Evidence in this record | Status |
| --- | --- | --- |
| XM2we | nqble's real-device checks in published HaloBattery pre-release e037304 | Battery comparison, charging display, sleep/wake and receiver reconnection observed |
| XM2w 4k | Mqtteo0's public checks in the original Stage D build; local automated checks | Battery and charging checks passed; later detection loss reported, recovery unresolved |
| XM2w 4k v2 | Experimental integration build | Janlhin’s private hardware summary awaits final wording approval |
| Other XM/OP1 models | No completed HaloBattery hardware results recorded here | Not established by this record |

- [XM2we observations](xm2we.md)
- [4K integration status](4k-status.md)
- [Credits and evidence boundaries](credits-and-sources.md)

A matching percentage at one point does not calibrate battery accuracy. A successful battery read does not prove that the tray icon will recover correctly after sleep or reconnection, or that other firmware versions will work. These are battery reporting/compatibility observations, not battery capacity, runtime or health measurements.
