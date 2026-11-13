# Credits and evidence boundaries

- **Janlhin** maintains the [Endgame Gear Web Configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator). [Public issue #1](https://github.com/Janlhin/Endgame_Gear_Web_Configurator/issues/1) records their XM2we protocol investigation, fixes and collaboration with nqble. This is an external source, not nqble's code.
- **[Mqtteo0](https://github.com/Mqtteo0)** independently tested the original XM2w 4k Stage D build and [permitted a credited summary](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716900302). Credit covers their reported battery, charging and recovery observations, not protocol research or our proposed explanation. See [the current evidence summary](4k-status.md).
- **nqble** performed the XM2we owner tests and prepared the contribution and experimental integration with GPT assistance. AI-generated changes require review and hardware validation.
- **HaloBattery's upstream and community maintainers** provide the application and integration framework.
- **Vole contributors** provide public [protocol research](https://github.com/johanneszab/vole). Recovery evidence cited here is pinned and scoped to OP1w hardware, not XM2w validation.

**[Janlhin](https://github.com/Janlhin)** — original XM2w 4k and v2 hardware investigation, vendor comparisons, charging/sleep and stall observations, diagnostic source proposals and technical-summary review.

## Publication scope

Public sources are linked; private messages, raw reports, attachments and identifying machine details are not reproduced. Raw-data redistribution requires separate permission. Public source code remains subject to its license and notices; a findings summary does not grant reuse rights.

Public protocol background includes [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator), [mouse-battery-monitor's ENDGAME.md at revision 25871cce](https://github.com/stuffz/mouse-battery-monitor/blob/25871cce3a8266d8d2bc05b0ca81fbb74b3a38b4/docs/ENDGAME.md), and [Vole's protocol documentation](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md).

ENDGAME.md independently documents the millivolt field, five-step percentage scale, stale-buffer rule for `0x08` and wired Charging presentation. Vole's OP1w findings supplied investigative background; they were not treated as proof of XM2w behavior. Each project retains its own attribution and licence terms.
