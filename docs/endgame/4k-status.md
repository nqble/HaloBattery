# Experimental 4K integration status

nqble prepared focused portable HaloBattery test builds with GPT assistance. These releases are experimental; their existence does not establish general model support.

| Model | Download | Public status |
| --- | --- | --- |
| Original XM2w 4k | [Original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | Candidate build; hardware validation pending |
| XM2w 4k v2 | [V2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | Hardware results received; technical summary awaiting publication permission |

## Local checks and next steps

The original-model candidate passed 17 focused automated tests, packaged parser/synthetic-identity checks and a simulated tray check. Historical v2 replies used in parser tests are not original-model hardware evidence. These checks do not measure real-device accuracy or reliability.

The original model is the last model planned for this testing round. Once its results are available and publication scope is agreed, nqble plans one combined contribution for community-maintainer review. No merge or release date is guaranteed. The original and v2 packages are separate; no repeat v2 testing is requested.

Each ZIP contains the app runtime and English/Chinese instructions. Download the Windows ZIP, extract it entirely and retain the runtime folder. The GitHub tag/source archive alone is not a complete source snapshot of the modified test executable; review source excerpts and base information are in the packages.

## Executable scans

[Original executable report](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior): last reviewed 2026-11-05 Pacific, 4/68 detections including Microsoft. The sandbox summary showed no malware detections or dropped files, but did not establish successful initialization with the complete runtime. False positives have not been established.

[V2 executable report](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior): last reviewed 2026-11-05 Pacific, 3/71 detections. The same full-runtime execution limitation applies. Counts may change; consult each exact report. Neither report is a security clearance or a reason to disable protection.

## Sources and publication boundary

Public protocol context: [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) and [Vole](https://github.com/johanneszab/vole). Their public work is credited separately from nqble's integration. Protocol families and hardware verification scopes must not be conflated.

Device-specific findings supplied privately are withheld pending permission. No private messages, reports, logs or identifying machine details are published here. A credited technical summary and redistribution of raw evidence require separate agreement. Receiving a report is not permission to publish its contents.
