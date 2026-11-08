# Experimental 4K integration status

Last fact-checked: 2026-11-08 (Pacific).

nqble prepared portable HaloBattery test builds for the original XM2w 4k and v2 with GPT assistance. They are experimental builds, not a claim of released support. The original-model candidate now has an unresolved detection-loss report.

| Model | Download | Public status |
| --- | --- | --- |
| Original XM2w 4k | [Original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1) | Battery/charging checks passed; detection loss later reported |
| XM2w 4k v2 | [V2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1) | Hardware results received; Janlhin’s private hardware summary awaits final wording approval |

## Original XM2w 4k: independent owner checks

On 2026-11-07, **[Mqtteo0](https://github.com/Mqtteo0)** confirmed testing `HaloBattery-XM2w4k-Original-StageD-r1-Windows` from this fork. Their [public results](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) confirm:

- The wireless battery percentage matched the official Endgame Gear software.
- Connecting the charging cable displayed charging.
- Unplugging the cable restored the battery percentage.

In a [later report](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6722818667), Mqtteo0 said detection stopped and opening then closing the official Endgame software restored it. The cause and trigger are not established. Confirmation of the build used for this failure and before/after diagnostics have been requested in the same thread. The earlier battery and charging observations still stand, but reliable detection and recovery are not established.

The reported workaround restores detection; it does not show that the underlying fault is fixed.

These are owner-reported checks on one original-model setup. The comment does not specify the measured percentage, firmware versions or Windows version. It does not report sleep, receiver reconnection, long-term reliability or multiple-device behavior. No raw logs are reproduced here.

Mqtteo0 [approved this summary's scope and attribution](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302) for the findings pages and correction PR. These results are independent of Janlhin's testing and do not authorize publication of Janlhin's privately supplied findings.

## Automated checks

The original-model candidate passed 17 focused automated tests, checks of recorded replies and simulated mouse identities in the packaged app, plus a simulated tray check. Historical v2 replies used in parser tests are not original-model hardware evidence. These checks do not measure real-device accuracy or reliability.

## Upstream integration and next steps

Upstream [PR #363](https://github.com/HeyOkay/HaloBattery/pull/363) merged the community history into the original repository's `pre-release` branch on 2026-11-08. Follow-up [PR #365](https://github.com/HeyOkay/HaloBattery/pull/365) records the pending Endgame correction. These integrations do not include this fork's corrected 4K reader.

The intended correction PR will target upstream `pre-release`. Next steps are to investigate the detection-loss report, finish the remaining validation and obtain final wording approval for privately supplied findings. Keep troubleshooting in [community issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) and link that evidence in the correction PR. No merge or release date is promised.

## Using the test downloads

Each ZIP contains the app runtime and English/Chinese instructions. Download the Windows ZIP, extract it entirely and retain the runtime folder. The GitHub tag/source archive alone is not a complete source snapshot of the modified test executable; review source excerpts and base information are in the packages.

## Executable scans

[Original executable report](https://www.virustotal.com/gui/file/7d9953cc4faffce0fe2dc05a07bf8b6307f564d949f4e73af704eb8b78e16b3f/behavior): last reviewed 2026-11-05 Pacific, 4/68 detections including Microsoft. The sandbox summary showed no malware detections or dropped files, but did not establish successful initialization with the complete runtime. False positives have not been established.

[V2 executable report](https://www.virustotal.com/gui/file/d0a9527aa44d98fbd8ee543b9f4eced744437ca4cd5020180a5963bb660c698e/behavior): last reviewed 2026-11-05 Pacific, 3/71 detections. The same full-runtime execution limitation applies. Counts may change; consult each exact report. Neither report is a security clearance or a reason to disable protection.

## Sources and publication boundary

Public results are documented here, including nqble's XM2we checks and Mqtteo0's original XM2w 4k observations. Janlhin's privately supplied hardware findings will be added after Janlhin approves the final wording. This review requirement does not hold up publication of independently public or separately approved results.

Public protocol context: [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator) and [Vole](https://github.com/johanneszab/vole). Their public work is credited separately from nqble's integration. Protocol families and hardware verification scopes must not be conflated.

Device-specific findings supplied privately are withheld pending permission. No private messages, reports, logs or identifying machine details are published here. A credited technical summary and redistribution of raw evidence require separate agreement. Receiving a report is not permission to publish its contents.
