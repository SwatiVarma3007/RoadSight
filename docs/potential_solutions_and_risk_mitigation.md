# RoadSight — Potential Solutions and Risk Mitigation

**Status:** Proposed mitigation measures pending implementation and testing.

| Risk | Proposed mitigation | Verification method |
|---|---|---|
| Unreliable submerged-road sensing | Conduct sensor feasibility tests before finalizing the sensing design. | Compare readings against known road profiles under controlled water conditions. |
| Water-surface interference | Evaluate sensor readings under different water depths and surface conditions. | Record and compare repeated measurements. |
| Vehicle motion and vibration | Develop a stable mounting arrangement and investigate motion-related measurement changes. | Compare stationary and controlled-motion test results. |
| Poor data quality | Validate readings and flag missing, stale or invalid data as `UNKNOWN`. | Inject invalid inputs and verify safe status handling. |
| False positives and missed hazards | Develop and refine classification criteria using labelled test data. | Measure false-positive rate and missed-hazard rate on test scenarios. |
| Water, mud and vibration exposure | Design appropriate enclosure and mounting protection. | Inspect and test the assembly under controlled exposure conditions. |
| Excessive warning latency | Optimize local processing and keep the warning path independent of network availability. | Measure end-to-end sensor-to-warning latency on the Raspberry Pi. |

## Priority

The first priority is sensor feasibility. If the selected sensing arrangement cannot provide useful evidence of submerged-road irregularities, document the limitation and reconsider the sensing approach before committing to full fabrication.

**Safety principle:** `UNKNOWN` must never be treated as `NORMAL`. All mitigations remain proposed until supported by documented test results.
