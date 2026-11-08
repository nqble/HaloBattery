# Experimental 4K integration status

nqble prepared focused portable HaloBattery test builds with GPT assistance. These releases are experimental; their existence does not establish general model support.

| Model | Download | Public status |
| --- | --- | --- |
| Original XM2w 4k | [Original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | Independent battery/charging checks passed; broader validation pending |
| XM2w 4k v2 | [V2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | Hardware results received; final public wording awaiting contributor review |

## Original XM2w 4k: independent owner checks

On 2026-11-07, **[Mqtteo0](https://github.com/Mqtteo0)** confirmed testing `HaloBattery-XM2w4k-Original-StageD-r1-Windows` from this fork. Their [public results](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) confirm:

- The wireless battery percentage matched the official Endgame Gear software.
- Connecting the charging cable displayed charging.
- Unplugging the cable restored the battery percentage.

These are owner-reported checks on one original-model setup. The comment does not specify the measured percentage, firmware versions or Windows version. It does not report sleep, receiver reconnection, long-term reliability or multiple-device behavior. No raw logs are reproduced here.

Mqtteo0 [approved this summary's scope and attribution](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302) for the findings pages and correction PR. These results are independent of Janlhin's testing and do not authorize publication of Janlhin's privately supplied findings.

## Local checks and next steps

The original-model candidate passed 17 focused automated tests, packaged parser/synthetic-identity checks and a simulated tray check. Historical v2 replies used in parser tests are not original-model hardware evidence. These checks do not measure real-device accuracy or reliability.

The original model is the last model planned for this testing round. Once the remaining testing and final wording review are complete, nqble plans one combined correction PR. Upstream [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) proposes bringing community development back to the original repository. The intended destination is upstream `pre-release` after that integration merges; if the transition is still pending, coordinate the destination with maintainers before submitting. No merge or release date is guaranteed. The original and v2 packages are separate; no repeat v2 testing is requested.

Each ZIP contains the app runtime and English/Chinese instructions. Download the Windows ZIP, extract it entirely and retain the runtime folder. The GitHub tag/source archive alone is not a complete source snapshot of the modified test executable; review source excerpts and base information are in the packages.

## Executable scans

[Original executable report](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior): last reviewed 2026-11-05 Pacific, 4/68 detections including Microsoft. The sandbox summary showed no malware detections or dropped files, but did not establish successful initialization with the complete runtime. False positives have not been established.

[V2 executable report](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior): last reviewed 2026-11-05 Pacific, 3/71 detections. The same full-runtime execution limitation applies. Counts may change; consult each exact report. Neither report is a security clearance or a reason to disable protection.

## Sources and publication boundary

Public protocol context: [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) and [Vole](https://github.com/johanneszab/vole). Their public work is credited separately from nqble's integration. Protocol families and hardware verification scopes must not be conflated.

Device-specific findings supplied privately are withheld pending permission. No private messages, reports, logs or identifying machine details are published here. A credited technical summary and redistribution of raw evidence require separate agreement. Receiving a report is not permission to publish its contents.
