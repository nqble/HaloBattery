# Endgame Gear battery findings

English | [简体中文](README.zh-CN.md)

Maintained by [nqble](https://github.com/nqble). This fork records specific HaloBattery tests and integration work, not official Endgame Gear support.

## Model status

| Model | Evidence | Status |
| --- | --- | --- |
| XM2we | nqble's checks in published pre-release `e037304` | Battery comparison, charging, sleep/wake and receiver reconnection observed |
| Original XM2w 4k | Mqtteo0's public Stage D checks | Battery/charging checks passed; cursor movement and Refresh do not reliably restore battery reporting |
| XM2w 4k v2 | Private hardware results received | Janlhin's final wording approval pending |
| Other XM/OP1 models | No completed hardware results recorded here | Support not established by this record |

- [4K maintainer summary, recovery evidence and next step](4k-status.md)
- [XM2we environment and observations](xm2we.md)
- [Credits, sources and publication scope](credits-and-sources.md)

## Scope

Stage D means the portable application test used in this collaboration. Original-model and v2 builds are separate. Simulations do not establish hardware compatibility. Matching percentages do not establish capacity, health or long-term accuracy. A result for one model or firmware does not establish another's behavior.

Public or separately approved results can be documented now. Janlhin's private findings require final wording approval; sharing raw reports or logs requires separate permission.
