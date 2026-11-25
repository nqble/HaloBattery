# Endgame Gear battery findings

English | [简体中文](README.zh-CN.md)

Maintained by [nqble](https://github.com/nqble). This fork records specific HaloBattery tests and integration work, not official Endgame Gear support.

## Model status

| Model | Evidence | Status |
| --- | --- | --- |
| XM2we | nqble's checks in published pre-release `e037304` | Battery comparison, charging, sleep/wake and receiver reconnection observed |
| Original XM2w 4k | Janlhin's native and source-run tray checks; Mqtteo0's separate portable-build tests | Working reads, charging display and ordinary sleep recovery; persistent reporting stall remains unresolved |
| XM2w 4k v2 | Janlhin's earlier portable Stage D checks and later native/source-run diagnostics | Working reads and earlier six-check pass; later persistent stalls qualify the earlier result |
| Other XM/OP1 models | No completed hardware results recorded here | Support not established by this record |

- [4K maintainer summary, recovery evidence and next step](4k-status.md)
- [Combined original/v2 findings](4k-findings.md)
- [XM2we environment and observations](xm2we.md)
- [Credits, sources and publication scope](credits-and-sources.md)

Current integration: [PR #479 merged into upstream pre-release](https://github.com/HeyOkay/HaloBattery/pull/479), carrying guarded local diagnostics in place of the process-based preparation in [closed PR #428](https://github.com/HeyOkay/HaloBattery/pull/428). Normal 4K polling remains disabled. Reply freshness and persistent reporting stalls remain tracked in [issue #324](https://github.com/HeyOkay/HaloBattery/issues/324); earlier experimental packages are not general support.

## Scope

Stage D means the portable application test used in this collaboration. Original-model and v2 builds are separate. Simulations do not establish hardware compatibility. Matching percentages do not establish capacity, health or long-term accuracy. A result for one model or firmware does not establish another's behavior.

Only the agreed technical summary is intended for publication. Private messages and raw reports, logs or screenshots are excluded. Attribution does not imply product endorsement or guaranteed maintainer acceptance.
