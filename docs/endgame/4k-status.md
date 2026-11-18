# 4K correction: readings verified, recovery unresolved

Updated November 18, 2026 (Pacific). [Upstream draft PR #428](https://github.com/HeyOkay/HaloBattery/pull/428) is open against `pre-release`. Normal 4K polling remains disabled; this is held preparation, not released support.

## Maintainer summary

| Model | Hardware evidence | Current limitation |
| --- | --- | --- |
| Original XM2w 4k | Janlhin's native and source-run tray checks; Mqtteo0's separate portable-build tests | Working reads, charging display and ordinary sleep recovery; persistent reporting stall remains unresolved |
| XM2w 4k v2 | Janlhin's earlier portable Stage D checks and later native/source-run diagnostics | Working reads and earlier six-check pass; later persistent stalls qualify the earlier result |

These are specific units and firmware, not lineup-wide validation. See the [approved detailed findings](4k-findings.md) for setups, protocol evidence, per-model results and limitations.

The correction uses `FF01:0002`, report `0xA1`, identity `0x0E` and battery `0xB4`. Failed-status payloads are rejected; wired display shows Charging without a misleading percentage. Successful replies have no verified command/sequence correlation, so stale successes can pass framing and repeated-value checks. Sample agreement does not prove freshness. No automatic `0x0F` recovery is implemented.

## Latest public hardware evidence

[Mqtteo0's November 13 report and paired diagnostics](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6849573528) identify the original-model **bounded-r1** build:

| Before opening the Endgame tool | After opening it and refreshing HaloBattery |
| --- | --- |
| Identity `0x0E` returned `0x08`; no validated battery sample | Accepted 55% receiver reading; mouse firmware bytes `01 10` |
| One 63-byte response; whole read attempt about 187 ms | Recovery was associated with vendor-tool use and Refresh |

This returned promptly; it is **not a captured timeout**. The recurrence shows that bounded-r1 has not eliminated the reporting failure. The owner describes PC startup; Restart versus shutdown/power-on, mouse state and the cause remain unconfirmed. Do not call this incident a proven sleep or Fast Startup bug, or infer recovery latency from report timestamps.

Earlier [battery/charging checks](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6716473809) remain useful. The [November 12 pair of accepted 25% readings](https://github.com/ahmedkhursheed23/HaloBattery/issues/48#issuecomment-6810893248) captured no failing-to-recovered sequence and did not establish a fix.

## Software checks are separate from hardware recovery

- **Published bounded-r1:** original model only; process isolation contains some blocked requests. It does not contain Janlhin's separate worker-thread timeout patch.
- **Upstream draft preparation:** PR #428 now carries the corrected reader and process isolation. Head `7491e04` adds cleanup-error containment so filesystem cleanup failures do not discard a valid reading. Normal polling remains held; reply freshness and persistent `0x08` recovery are unresolved.
- **Software evidence for PR #428:** the latest local PR source suite ran **2,339 tests, two skipped**; GitHub tests also passed. A previously frozen build at `769727f` passed seven fake-device worker cases, including original/v2 success, status rejection and blocked open/send/read/close. That frozen dispatch check predates the cleanup-only follow-up; it is not a new owner build or full installer acceptance test.
- These checks establish bounded software behavior, not hardware recovery or general compatibility. Failed termination or abrupt exit can still leave worker files. No new hardware test or download is implied.
- The older candidate at `a4159e8` and its 2,017-test/package results are historical; they are not the current PR snapshot.

Janlhin's separate corrected timeout patch remains software-tested only; its exact identity and evidence boundaries are in the detailed findings. Do not combine its test counts with the process-isolation candidate's results.

## Next evidence needed

Identify what the official tool does when reporting resumes. An optional capture method is prepared, not executed: prepare receiver-only USB capture before a failure, record one natural failure, check whether reopening HaloBattery alone restores it, then capture vendor-tool-associated recovery with only one reader running at a time. No new test results or tester agreement are implied.

Keep raw captures private pending review. A display filter is not anonymization. Do not replay unknown vendor commands or add `0x0F` from the OP1w analogy. A recovery claim needs a captured failure, supported action, accepted readings afterward and repeatable behavior without unwanted wake/sleep changes.

## Downloads and context

Experimental packages: [original Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-stage-d-r1), [v2 Stage D](https://github.com/nqble/HaloBattery/releases/tag/xm2w4kv2-stage-d-r1), [original bounded-r1](https://github.com/nqble/HaloBattery/releases/tag/xm2w4k-original-bounded-r1). Extract the entire runtime ZIP. Older executable scans do not cover the current PR source; no scan was rechecked for this update.

[Earlier investigation chronology](https://github.com/nqble/HaloBattery/blob/4c52344615015b2b81832f96b647090d457439a9/docs/endgame/4k-status.md) retains the dated diagnostics and older packaging checks.

**Current tracking:** [upstream issue #324](https://github.com/HeyOkay/HaloBattery/issues/324) and [draft PR #428](https://github.com/HeyOkay/HaloBattery/pull/428). [Community issue #48](https://github.com/ahmedkhursheed23/HaloBattery/issues/48) remains the earlier public testing record. HeyOkay [consolidated duplicate #321 into #324](https://github.com/HeyOkay/HaloBattery/issues/324#issuecomment-6974465678); its older `FF02:0002 / query 04` short-send report is not a test of the corrected path or new evidence of its stall. Closing that duplicate does not mean support is enabled or fixed. No merge, release date or safe automatic recovery is promised.

Hardware research: **Janlhin**. Independent public testing: **Mqtteo0**. Integration and packaging: **nqble**, with GPT assistance. See [credits and source boundaries](credits-and-sources.md). Only approved summaries are public; private reports, logs and messages are excluded.
