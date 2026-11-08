# XM2we — nqble's observations

Tested by nqble, using the published HaloBattery pre-release identified as e037304. This is a summary of the owner's observations, not a universal compatibility claim.

## Test environment and scope

| Item | Recorded detail |
| --- | --- |
| Tester | nqble |
| Mouse / connection | XM2we through its original 2.4 GHz receiver, VID 0x3367 / PID 0x1961 |
| HaloBattery build | Published pre-release e037304, app version 1.16.0 |
| Runtime in the saved app diagnostics | Python 3.12.10, win32 |
| Windows version checked on 2026-11-06 | 23H2, build 22631.6199; current-system readout, not a historical record of the earlier session |
| Mouse / receiver firmware | Not confirmed by the retained evidence |
| Settings during the published-build check | Approximately one-minute polling interval |

The earlier configurator export identifies Windows/Chrome but not an exact Windows build. Its generic device/parsed fields include unconfirmed defaults; WE-specific data and logs are the relevant evidence. The official tool's displayed Driver version 1.0 is not a confirmed mouse/receiver firmware version. A downloaded firmware updater does not establish the installed version.

## Published HaloBattery build observations

| Check | Observed result |
| --- | --- |
| Wireless percentage | HaloBattery and the official tool both displayed 85% |
| Cable connection | Charging indicator appeared within a couple of seconds |
| Cable removal | Charging remained until manual refresh or the next one-minute poll |
| Receiver reconnection | Detection returned after mouse movement |
| Natural sleep/movement | Sleep indicator appeared during testing; movement restored the normal indicator |

The sleep duration was not measured in this session. Exact voltage, charging current, battery capacity and long-term accuracy were not established. Do not infer direct-USB provider coverage from seeing a charging indication while a receiver is present. Installed firmware remains unconfirmed; the current Windows readout is distinguished from the original test environment above.

Public follow-up: [HaloBattery issue #12](https://github.com/ahmedkhursheed23/HaloBattery/issues/12).
Contribution: [PR #13](https://github.com/ahmedkhursheed23/HaloBattery/pull/13).

Earlier configurator work with Janlhin covered a different application and separate tests: [public issue #1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1). Those results should not be counted as HaloBattery tray validation.

## Separate public configurator testing

In [Janlhin's public issue #1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1), nqble tested XM2we configuration reading/writing over both wired PID 0x1960 and receiver PID 0x1961. Official-tool LOD changes from 2 mm to 1 mm and back to 2 mm isolated EEPROM byte 0x0A and its checksum 0x0B; the restored 181-byte image matched the baseline. Subsequent configurator LOD writes were checked against read-back, the official tool and a perceived physical lift-off difference; exact heights were not measured. Final wireless verification on build 9e3389c confirmed unchanged performance settings sent no writes and restoration returned the entire image to the baseline.

These are nqble's publicly documented owner tests in Janlhin's configurator, not additional HaloBattery provider coverage. Janlhin's investigation and fixes are credited in the linked discussion and the credits page. No private 4K findings or raw files are included here.
