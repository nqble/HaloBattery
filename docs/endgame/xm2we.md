# XM2we — nqble's observations

Tested by nqble, using the published HaloBattery pre-release identified as e037304. This is a summary of the owner's observations, not a universal compatibility claim.

| Check | Observed result |
| --- | --- |
| Wireless percentage | HaloBattery and the official tool both displayed85% |
| Cable connection | Charging indicator appeared within a couple of seconds |
| Cable removal | Charging remained until manual refresh or the next one-minute poll |
| Receiver reconnection | Detection returned after mouse movement |
| Natural sleep/movement | Sleep indicator appeared during testing; movement restored the normal indicator |

The sleep duration was not measured in this session. Exact voltage, charging current, battery capacity and long-term accuracy were not established. Do not infer direct-USB provider coverage from seeing a charging indication while a receiver is present. Firmware and OS versions are not recorded in this summary.

Public follow-up: [HaloBattery issue12](https://github.com/ahmedkhursheed23/HaloBattery/issues/12).
Contribution: [PR13](https://github.com/ahmedkhursheed23/HaloBattery/pull/13).

Earlier configurator work with Janlhin covered a different application and separate tests: [public issue1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1). Those results should not be counted as HaloBattery tray validation.
