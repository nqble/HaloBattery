# Experimental 4K integration status

Last recovery-status update: 2026-11-10 (Pacific). Other dated checks retain their stated dates.

nqble prepared portable HaloBattery test builds for the original XM2w 4k and v2 with GPT assistance. They are experimental builds, not a claim of released support. Original-model battery and charging checks passed, but detection recovery is inconsistent and unresolved on one reported setup.

| Model | Download | Public status |
| --- | --- | --- |
| Original XM2w 4k | [Original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | Battery/charging checks passed; detection recovery inconsistent and unresolved |
| XM2w 4k v2 | [V2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | Hardware results received; Janlhin’s private hardware summary awaits final wording approval |

## Original XM2w 4k: independent owner checks

On 2026-11-07, **[Mqtteo0](https://github.com/Mqtteo0)** confirmed testing `HaloBattery-XM2w4k-Original-StageD-r1-Windows` from this fork. Their [public results](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) confirm:

- The wireless battery percentage matched the official Endgame Gear software.
- Connecting the charging cable displayed charging.
- Unplugging the cable restored the battery percentage.

Mqtteo0 initially [reported detection loss](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6722818667). On [November 9](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6742865971), they reported standby followed by recovery after movement and waiting or Refresh. In their [November 10 follow-up](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6764152209), movement had worked the previous day, but opening the official tool now seemed necessary each time.

Recovery remains unresolved. In the [later November 10 reply with paired diagnostics](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6777323188), Mqtteo0 suspects idle time because they frequently use a gamepad, but is not certain. Waiting time, a failed manual Refresh, and normal cursor input during failure are still unconfirmed. Polling has not been shown to cause sleep; receiver-replug, long-term and multiple-device checks remain unreported.

The before report has no current battery result and records `device status 0x08; payload not used`. The receiver remains listed as `VID=3367 PID=1970`, including `FF01:0002`. The after report from the same original Stage D r1 build shows 45% via the receiver, with charging status unknown. The report timestamps are 34 seconds apart; that is not a measured recovery latency from mouse movement or tool launch.

In the candidate parser, `0x08` is a non-success status and its payload is rejected; these reports do not decode its precise cause. The failure snapshot therefore shows an enumerated receiver and a protocol status response, not merely an absent USB device or tray icon. Historical input-triggered polling entries do not prove that the XM mouse itself was moving at the failed snapshot.

### Related protocol evidence: model scope matters

[Vole section 14](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md#14-a-failed-command-wedges-the-device-until-the-next-probe) reports failed-command communication lockup cleared by a successful `0x0F` probe. Its live evidence is OP1w 4k v2, mouse firmware 1.07 and receiver firmware 1.01 on Linux—not original XM2w 4k validation.

This is a plausible recovery mechanism, not a confirmed explanation of Mqtteo0's report. Our candidate permits only `0x0E` and `0xB4`; no probe fallback has been added. Nine targeted simulated tests passed, including checks showing that current diagnostics cannot distinguish identity-request failure from battery-request failure. A separate diagnostic-only proposal adds command/status/length/timing information without changing device requests. Neither hardware recovery nor a new executable has been tested.

## Working hypothesis: not a finding

Normal mouse input may resume while battery communication remains unavailable, with the official tool restoring that communication. This is an integration hypothesis, not an owner-confirmed observation. Possible explanations include reader recovery handling, device/receiver state, reopening communication, application interaction, or simply more elapsed time. No mechanism or original-model-specific defect has been established.

Paired diagnostics now narrow the failure to unsuccessful status communication with an enumerated receiver. Further useful checks are cursor movement during failure, whether manual Refresh succeeds, and repeat sleep/wake behavior with the official tool closed. These remain proposed checks, not completed tests or a request to send guessed wake commands. Earlier successful battery and charging checks remain valid.

The diagnostics attached to the November 9 clarification identify the original Stage D r1 build, show a successful 75% receiver reading and record input-triggered polling while a reading was greyed. That snapshot is not a simultaneous 75% comparison against the official tool. No raw logs or identifying machine details are reproduced here.

Mqtteo0 [approved this summary's scope and attribution](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302) for the findings pages and correction PR. These results are independent of Janlhin's testing and do not authorize publication of Janlhin's privately supplied findings.

## Automated checks

The original-model candidate passed 17 focused automated tests, checks of recorded replies and simulated mouse identities in the packaged app, plus a simulated tray check. Historical v2 replies used in parser tests are not original-model hardware evidence. These checks do not measure real-device accuracy or reliability.

## Upstream integration and next steps

Upstream [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) merged the community history into the original repository's `pre-release` branch on 2026-11-08. Follow-up [PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) records the pending Endgame correction. These integrations do not include this fork's corrected 4K reader.

The intended correction PR will target upstream `pre-release`. Next steps are to investigate inconsistent detection recovery, finish remaining validation and obtain final wording approval for private findings. Keep troubleshooting in [community issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) and link evidence in the correction PR. No merge or release date is promised.

## Using the test downloads

Each ZIP contains the app runtime and English/Chinese instructions. Download the Windows ZIP, extract it entirely and retain the runtime folder. The GitHub tag/source archive alone is not a complete source snapshot of the modified test executable; review source excerpts and base information are in the packages.

## Executable scans

VirusTotal reports last checked on 2026-11-08 Pacific:

- [Original executable](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior): 2/71 vendor detections; Microsoft reported Undetected.
- [V2 executable](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior): 3/71 vendor detections.

Both behavior reports showed one medium Sigma match, Potential Python DLL SideLoading, and no malware detections or dropped files in the activity summary. At least one run in each report explicitly failed to load `_internal\python312.dll`; those runs did not start the complete app. The reports do not establish a clean execution of the full portable package or confirm false positives. Counts can change; neither report is a security clearance or a reason to disable protection.

## Sources and publication boundary

Public results are documented here, including nqble's XM2we checks and Mqtteo0's original XM2w 4k observations. Janlhin's privately supplied hardware findings will be added after Janlhin approves the final wording. This review requirement does not hold up publication of independently public or separately approved results.

Public protocol context: [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) and [Vole](https://github.com/johanneszab/vole). Their public work is credited separately from nqble's integration. Protocol families and hardware verification scopes must not be conflated.

Device-specific findings supplied privately are withheld pending permission. No private messages, reports, logs or identifying machine details are published here. A credited technical summary and redistribution of raw evidence require separate agreement. Receiving a report is not permission to publish its contents.
