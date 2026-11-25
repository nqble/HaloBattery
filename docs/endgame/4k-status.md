# 4K correction: readings verified, recovery unresolved

Updated November 25, 2026 (Pacific). [PR #479](https://github.com/HeyOkay/HaloBattery/pull/479) merged into upstream `pre-release` on November 22. It carries the sourced A1 protocol preparation through guarded local diagnostics. [PR #428 was closed as superseded](https://github.com/HeyOkay/HaloBattery/pull/428#issuecomment-7079239539), with credit to nqble, Janlhin and Mqtteo0. Normal 4K polling remains disabled; merged diagnostics are not released battery support.

## Maintainer summary

| Model | Hardware evidence | Current limitation |
| --- | --- | --- |
| Original XM2w 4k | Janlhin's native and source-run tray checks; Mqtteo0's separate portable-build tests | Working reads, charging display and ordinary sleep recovery; persistent reporting stall remains unresolved |
| XM2w 4k v2 | Janlhin's earlier portable Stage D checks and later native/source-run diagnostics | Working reads and earlier six-check pass; later persistent stalls qualify the earlier result |

These are specific units and firmware, not lineup-wide validation. See the [approved detailed findings](4k-findings.md) for setups, protocol evidence, per-model results and limitations.

The correction uses `FF01:0002`, report `0xA1`, identity `0x0E` and battery `0xB4`. Failed-status payloads are rejected. Earlier test builds withheld the wired percentage; the replacement diagnostic also withholds it and labels cable-based charging as inference, not a verified charging flag. Successful replies have no verified command/sequence correlation, so stale successes can pass framing and repeated-value checks. Sample agreement does not prove freshness. No automatic `0x0F` recovery is implemented.

## Latest public hardware evidence

[Mqtteo0's November 13 report and paired diagnostics](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6849573528) identify the original-model **bounded-r1** build:

| Before opening the Endgame tool | After opening it and refreshing HaloBattery |
| --- | --- |
| Identity `0x0E` returned `0x08`; no validated battery sample | Accepted 55% receiver reading; mouse firmware bytes `01 10` |
| One 63-byte response; whole read attempt about 187 ms | Recovery was associated with vendor-tool use and Refresh |

This returned promptly; it is **not a captured timeout**. The recurrence shows that bounded-r1 has not eliminated the reporting failure. The owner describes PC startup; Restart versus shutdown/power-on, mouse state and the cause remain unconfirmed. Do not call this incident a proven sleep or Fast Startup bug, or infer recovery latency from report timestamps.

Earlier [battery/charging checks](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) remain useful. The [November 12 pair of accepted 25% readings](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6810893248) captured no failing-to-recovered sequence and did not establish a fix.

## Integrated diagnostics versus earlier builds

- **Current upstream implementation:** [merge c2e363a](https://github.com/HeyOkay/HaloBattery/commit/c2e363abb196d25fd3825c3476931247550644fd) uses the shared in-process transport, not #428's worker processes. Normal `poll()` returns no reading and performs no enumeration or device access.
- **Explicit diagnostics only:** the user must acknowledge experimental operation and select receiver or wired transport. Ambiguous endpoints are refused. Close HaloBattery and vendor tools first; the app lease does not exclude vendor software. See the [upstream diagnostic instructions](https://github.com/HeyOkay/HaloBattery/blob/c2e363abb196d25fd3825c3476931247550644fd/docs/device-diagnostics.md), not the older package instructions.
- **Evidence limits:** identity is queried before one battery `0xB4` request; repeated values are not treated as freshness proof. No automatic recovery query is sent. A failed exchange may require replugging or vendor-tool recovery. Diagnostic readings do not create normal tray status or enable the device family.
- **Upstream-reported checks:** #479 reports 3,697 offline tests with three optional skips and Ruff passing. These are the maintainer's software results, not independently rerun here or new hardware evidence. This November 25 update inspects source and tests; it sends no device requests.
- **Historical packages:** published bounded-r1 is original-model only and uses process isolation. #428 at `7491e04` had 2,339 tests with two skipped; an earlier frozen build at `769727f` passed seven fake-device worker cases. Those results belong to those implementations and do not validate #479's transport. No new owner build, download or scan is supplied by this update.

Janlhin's corrected timeout patch remains separate, software-tested evidence. Do not combine its counts with either upstream implementation. The approved model findings and their hardware limitations are unchanged.

## Next evidence needed

Identify what the official tool does when reporting resumes. An optional capture method is prepared, not executed: prepare receiver-only USB capture before a failure, record one natural failure, check whether reopening HaloBattery alone restores it, then capture vendor-tool-associated recovery with only one reader running at a time. No new test results or tester agreement are implied.

Keep raw captures private pending review. A display filter is not anonymization. Do not replay unknown vendor commands or add `0x0F` from the OP1w analogy. A recovery claim needs a captured failure, supported action, accepted readings afterward and repeatable behavior without unwanted wake/sleep changes.

## Downloads and context

Experimental packages: [original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1), [v2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1), [original bounded-r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-bounded-r1). Extract the entire runtime ZIP. Older executable scans do not cover the current PR source; no scan was rechecked for this update.

[Earlier investigation chronology](https://github.com/nqble/HaloBattery/blob/4c52344615015b2b81832f96b647090d457439a9/docs/endgame/4k-status.md) retains the dated diagnostics and older packaging checks.

**Current tracking:** [upstream issue #324](https://github.com/HeyOkay/HaloBattery/issues/324). [Merged PR #479](https://github.com/HeyOkay/HaloBattery/pull/479) carries diagnostics; [closed PR #428](https://github.com/HeyOkay/HaloBattery/pull/428) preserves the earlier review record. [Community issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) remains the earlier public testing record. HeyOkay [consolidated duplicate #321 into #324](https://github.com/HeyOkay/HaloBattery/issues/324#issuecomment-6974465678); its older `FF02:0002 / query 04` short-send report is not a test of the corrected path or new evidence of its stall. Closing that duplicate does not mean support is enabled or fixed. The diagnostic merge does not resolve normal support, a release date or safe automatic recovery.

Hardware research: **Janlhin**. Independent public testing: **Mqtteo0**. Integration and packaging: **nqble**, with GPT assistance. See [credits and source boundaries](credits-and-sources.md). Only approved summaries are public; private reports, logs and messages are excluded.
