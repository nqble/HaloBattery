# XM2w 4k and XM2w 4k v2 — readings work; persistent stalls remain unresolved

English | [简体中文](4k-findings.zh-CN.md)

Janlhin verified the read-only battery path on one original XM2w 4k and one XM2w 4k v2. Model identity, mouse firmware, receiver firmware and wireless percentage agreed with vendor-tool cross-checks in the tested sessions. Both units also developed a persistent status-reporting stall. Working reads therefore establish compatibility with the tested path, not reliable recovery or readiness for general release.

## Tested setups

| Item | Original XM2w 4k | XM2w 4k v2 |
| --- | --- | --- |
| Identity PID | `0x1968` | `0x1982` |
| Mouse firmware | `01 10`, displayed as 1.10 by the vendor tool | `01 07`, displayed as 1.07 |
| Receiver firmware | 1.01 | 1.01 |
| Vendor comparison tool | 1.04 | 1.02 |
| Operating system | Windows 11 build 26220.9757 | Windows 11 build 26220.9757 |
| Scope | One mouse and receiver pair | One mouse and receiver pair |

The initial v2 native and Stage D sessions were on November 5–6, 2026. Later diagnostic sessions covered both models on November 11 and additional v2 probes on November 12, using UTC+8 dates. Findings from different runs are kept distinct.

## Shared working path

The tested path uses VID `0x3367`, collection `0xFF01:0002` and feature report `0xA1`. Identity command `0x0E` identifies the model; battery command `0xB4` carries percentage at offset 16. Receiver-information command `0x0D` was used in the later diagnostic work.

Observed responses include explicit `0xA1` reports of 63 and 64 bytes. Some early records were normalized; separate direct reads also returned 63 bytes. This supports handling those observed layouts while retaining report-ID, status, length and field-bounds validation. It does not justify padding replies or accepting arbitrary layouts.

Failed replies can retain the payload of an earlier successful identity or battery response. A returning `0x08` reply must not be interpreted as a current battery sample. Reply presence alone does not establish that the requested mouse status was obtained.

Wired percentage differed substantially from wireless percentage, so the candidate displays **Charging** without a number on the wired path. This label is inferred from the connection, not a decoded charging flag. Neither these comparisons nor the reported voltage changes establish calibrated capacity or runtime.

Wireless values sometimes differed between nearby samples. Earlier v2 data included one 35% sample in fourteen total samples, with the other thirteen at 40%; later original-model readings alternated between 70% and 75%. Requiring two consecutive agreeing values within three attempts is the candidate's consistency policy, not a hardware rule established by these measurements.

## Original XM2w 4k

Wireless reads matched the vendor tool at 75%; later native and tray reads showed 80% in a separate part of the session. The cabled body exposes PID `0x1968` on the same vendor collection. Including that PID allowed the diagnostic tree to switch between wired charging text and wireless percentage, with one device icon and automatic return after cable removal.

That wired-enumeration omission affected the v2-derived diagnostic tree used for these measurements. The separately prepared original-model portable builds already included PID `0x1968`; this finding does not establish the same omission in those builds.

Ordinary sleep was observed after about 3.5 minutes in one run, followed by recovery on movement. Separately, Janlhin recorded three persistent stalls: cursor movement continued, but status commands returned `0x08` and movement did not restore reporting. One occurrence arose during the application's normal 60-second polling, without a special high-frequency test harness.

One uncontrolled occurrence recovered after movement and a mouse-targeted `0x0F` probe. This is an observed association, not proof that either action is necessary or sufficient. The clarified helper's `None` output means accepted status `0x01`; it does not mean no response or provide a battery value.

## XM2w 4k v2

The earlier portable Stage D session reported that all six requested checks passed. It showed the correct name and 100%, charging text without a number, and one icon. The earlier native/vendor comparison was at 35%; it is a different measurement.

Sleep was observed at about 2.7 minutes in Stage D and 3.1–3.6 minutes in a separate native run. Later diagnostic observations were shorter again. These are run-specific observations, not fixed sleep timers or proof of a consistent speed difference between models.

The earlier receiver removal-to-recovery interval was about 75 seconds, including a deliberate 10-second unplugged wait, reinsertion, detection and polling. It is not a measurement of re-enumeration latency alone. Offline icon removal after about five minutes was one observation, not a verified upper bound.

The later work recorded two persistent stalls on this unit. Movement did not restore status reads; opening the vendor tool was followed by successful reads. Four `0x0F` attempts produced three failures and one uncontrolled success. The success had incomplete movement instrumentation and was not reproduced by the later controlled attempts. A 360-second no-probe control did not recover during that interval; it does not establish that spontaneous recovery is impossible.

## What remains unresolved

The persistent stall is distinct from ordinary sleep: movement can restore normal sleep reads, but did not clear the recorded stalls. Vendor-tool recovery was observed, but the responsible action is unknown. The inconsistent probe results do not establish a safe automatic recovery sequence; no automatic `0x0F` recovery is proposed here.

Status `0x11` was observed after some probes, but its exact meaning remains unverified. A channel-resynchronization explanation and a shared-buffer explanation for cross-process interference remain hypotheses. The evidence does not establish either mechanism or prove that all detection loss is the same failure.

The later assigned receiver unplug/replug experiment remains pending. Disconnecting invalidated the HID handle and raised `OSError`; substituting mouse power-off was not equivalent. This does not erase the earlier v2 Stage D reconnection observation. No additional hardware testing is currently requested.

Two receivers together triggered the diagnostic provider's multi-device guard. Multi-unit association, other firmware, other Endgame models, long-term reliability and battery calibration remain outside this evidence set.

## Source and timeout boundaries

Later measurements used a local diagnostic tree based on `e037304`, labelled `xm2w4kv2-stageD-r1+0d`, with the cumulative correction and original-model wired support. It has no separate Git revision. The diagnostic command logs used its Reader; Stage D used the tray from source. The November 12 v2 probes used standalone hidapi scripts without the provider loaded.

Janlhin's same-name corrected timeout patch, revision 2 (SHA-256 `e14a9ad962e9018888daf07fbf803f55a23bd05747047c2a76a6babf517db9f4`), was created after all hardware work. It retains an outstanding worker and its handle, prevents reopening that path while the worker runs, and bounds diagnostic `0x0D` sending as well as reading. Janlhin reports 12 simulated-device tests and a full run of 1,796 tests with two skipped. nqble has inspected the repairs but has not independently rerun that suite.

That patch has no hardware, tray or packaged-build validation. Its two-second ceiling applies to individual send/read calls, not every operation or the whole poll. A worker that never returns still leaves the path unavailable. It is a robustness proposal, not evidence of a fix for returning `0x08` stalls.

nqble's released `xm2w4k-original-bounded-r1` uses a separate process-isolation design and supports the original model only. It does not contain Janlhin's timeout patch. Independently, [Mqtteo0's public testing](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) includes reporting loss, vendor-tool-associated recovery and a later successful Refresh/read with the bounded build. Successful reads alone do not establish a stall fix or validate timeout handling.

## Credit and sources

Hardware investigation, measurements and implementation recommendations: **[Janlhin](https://github.com/Janlhin)**. Candidate integration, packaging and coordination with GPT assistance: **[nqble](https://github.com/nqble)**. Independent original-model testing and public diagnostics: **[Mqtteo0](https://github.com/Mqtteo0)**.

Public protocol background includes [Janlhin's configurator](https://github.com/Janlhin/Endgame_Gear_Web_Configurator), [mouse-battery-monitor's ENDGAME.md at revision 25871cce](https://github.com/stuffz/mouse-battery-monitor/blob/25871cce3a8266d8d2bc05b0ca81fbb74b3a38b4/docs/ENDGAME.md), and [Vole's protocol documentation](https://github.com/johanneszab/vole/blob/4ba29dea54b4628df03cfe2f94f4576c124afd80/re/PROTOCOL.md).

ENDGAME.md independently documents the millivolt field, five-step percentage scale, stale-buffer rule for `0x08` and wired Charging presentation. Vole's OP1w findings supplied investigative background; they were not treated as proof of XM2w behavior. Each project retains its own attribution and licence terms.

Only the agreed technical summary is intended for publication. Private messages and raw reports, logs or screenshots are excluded. Attribution does not imply product endorsement or guaranteed maintainer acceptance.
