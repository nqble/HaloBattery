# Experimental 4K integration

Recovery evidence updated 2026-11-11 (Pacific). Stage D builds are experimental, not released support.

## Maintainer summary

| Model | Evidence | Remaining work |
| --- | --- | --- |
| Original XM2w 4k | Mqtteo0 confirmed battery agreement, charging display and recovery after cable removal | Battery reporting can remain unavailable despite cursor movement and Refresh; opening the official tool restores it |
| XM2w 4k v2 | Private hardware results received | Janlhin must approve the final public wording |

The candidate uses `FF01:0002`, report `0xA1`, identity command `0x0E` and battery command `0xB4`. Non-success payloads are rejected. No `0x0F` probe or hardware-tested recovery fix has been added.

## Original-model hardware evidence

**[Mqtteo0](https://github.com/Mqtteo0)** tested `HaloBattery-XM2w4k-Original-StageD-r1-Windows`. Their [November 7 results](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) confirm wireless percentage agreement with the official tool, charging display on cable connection, and percentage recovery after cable removal.

Recovery was initially reported after [movement and waiting or Refresh](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6742865971). On November 10, [opening the official tool seemed necessary](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6764152209). The [November 10 reply](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6782283052) confirms cursor movement but failed recovery through Refresh.

The [paired diagnostics](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6777323188) show:

| Before opening the official tool | After opening it |
| --- | --- |
| No battery result; `device status 0x08; payload not used` | Successful 45% receiver reading; charging status unknown |
| Receiver `VID=3367 PID=1970`, including `FF01:0002`, remains listed | Same original Stage D r1 build |

Idle is suspected, not confirmed. The 34-second gap between report timestamps is not measured recovery latency. An earlier 75% snapshot was not a simultaneous official-tool comparison. Receiver-replug, long-term and multiple-device checks remain unreported. The recovery issue does not invalidate the earlier battery/charging checks.

## Recovery hypothesis and software checks

Battery communication may remain stuck after a failed request. [Vole section 14](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md#14-a-failed-command-wedges-the-device-until-the-next-probe) describes recovery through `0x0F`, but its live evidence is **OP1w 4k v2, mouse FW 1.07 / receiver FW 1.01 on Linux**. This is a lead, not an established XM2w cause or fix. Device state, application interaction and elapsed time remain alternatives.

The [logging build](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-logging-r1) identifies the failing command without adding device commands. [November 11 diagnostics](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6803300510) show identity command `0x0E` returning `0x08` before and after restarting HaloBattery. After opening the official tool, a battery request returns `0x01`, but that poll still fails the consecutive-sample agreement check. The displayed 30% is cached, not a newly accepted reading.

These failures returned promptly; they do not demonstrate a blocked HID call. The reported elapsed time covers the whole read attempt, not just the final request.

### Published original-model timeout experiment

The [original-model bounded-r1 build](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-bounded-r1) runs status transactions in a separate process. Its earlier local checks passed: 29 focused tests, seven packaged worker simulations and a synthetic tray check. It supports the original model only and has not been submitted to VirusTotal.

[Mqtteo0's subsequent report](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6810893248) says Refresh worked without the official tool. Both attached snapshots contain an accepted online 25% reading. They do not capture a failure-to-recovery sequence or a timeout, so they do not establish that the intermittent reporting loss is fixed.

### Current-upstream packaging verification

A separate local candidate is based on upstream pre-release `db0516e6ab5f50706385d50ffc20b4b9e10071a8`. It prepares original/v2 identity handling and process-isolated status transactions, while retaining the release hold: normal 4K polling remains disabled.

The updated source suite passed: **1,988 tests run, two skipped**. Packaged verification passed ten simulated transactions, including both model identities, wired presentation, failure status, sample disagreement and hangs during open/send/read/close. Five lifecycle checks cover concurrent-request refusal, pending termination, completed-worker cleanup, active shutdown and closed-boundary suppression; pending-termination and completed-worker cases use simulated process objects. A synthetic tray check and three additional canonical worker-entry cases passed. Embedded code matched the reviewed source.

The first tray attempt failed to create its Windows notification-area icon in the restricted execution context. Retrying in the normal desktop context passed; the initial failure is retained in the local verification record. These are software simulations, not new mouse hardware results.

After launch, the parent waits up to eight seconds for transaction completion, then attempts termination and cleanup. An unreaped worker blocks another transaction. Parent enumeration and process creation are outside that wait; abrupt process exit and unusual driver/OS termination remain unverified. Only `0x0E` and `0xB4` are allowed; no `0x0D` follow-up or automatic `0x0F` recovery was added.

This candidate and its local verification harness are **not a new tester release**. Do not send the harness as a hardware-test build. A separately prepared portable test package and short checklist are needed before asking an owner to test. The persistent returning-`0x08` stall remains unresolved; blocking-call protection does not establish recovery.

### Investigation plan

The working explanation is that cursor input recovers while battery communication remains stuck; opening the official tool appears to restore reporting. What the tool changes is unknown. No fix has been confirmed.

1. Review the packaged candidate, then prepare a separately labelled portable package and focused hardware checklist. Keep timeout protection separate from investigation of returning `0x08` responses.
2. Capture individual battery samples when communication resumes but the agreement check fails. Do not infer their values from the cached percentage.
3. Review model-specific sleep effects and request details before considering a controlled `0x0F` experiment. No automatic probe fallback is implemented or approved by this plan.

A separate option is to investigate receiver notifications for sleep/wake and battery changes, potentially avoiding queries during sleep. [Vole's protocol notes](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md) describe a separate Windows notification collection, `FF02:0001`; `FF01:0002` remains the command channel. Equivalent XM2w behavior and coexistence with other software are unverified. No notification reader has been implemented.

Acceptance requires repeated recovery without the official tool, preserved battery/charging behavior and no unwanted wake or delayed sleep. A single successful reading is insufficient.

## Integration and next step

Upstream [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) merged community history into `pre-release` on November 8; [PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) noted the pending Endgame correction. Neither included this candidate reader. No correction PR from nqble was listed upstream when checked on November 10.

Investigate recovery, finish validation and obtain approval for private findings before submitting the combined correction to upstream `pre-release`. Troubleshooting remains in [issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48). No merge or release date is promised.

## Downloads and dated scans

- [Original XM2w 4k Stage D r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1)
- [XM2w 4k v2 Stage D r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1)

Extract the entire Windows ZIP and retain its runtime folder. English/Chinese instructions are included. The tag source archive is not a complete snapshot of the modified executable; packages include review excerpts and base information.

VirusTotal last checked **November 8**, not rechecked for this update: [original](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior) 2/71 detections; [v2](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior) 3/71. Both had a medium Python DLL sideloading Sigma match and at least one `_internal\python312.dll` load failure. Neither proves successful full-app execution or confirmed false positives. Counts can change; do not disable protection on this basis.

## Attribution and publication

Mqtteo0 [permitted a credited technical summary](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302). Their public observations are separate from our hypotheses and Janlhin's private results. See [credits and evidence boundaries](credits-and-sources.md). No raw reports or identifying machine details are reproduced here.
