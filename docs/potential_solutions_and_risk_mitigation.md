# RoadSight — Potential Solutions and Risk Mitigation



## 1. Risk Assessment and Mitigation

| Risk | Proposed Mitigation | Verification Method |
|---|---|---|
| Unreliable submerged-road sensing | Conduct sensor feasibility tests before finalising the sensing design. | Compare measurements against known road profiles under controlled water conditions. |
| Water-surface interference | Evaluate sensing performance under different water depths and surface conditions. | Record and compare repeated measurements. |
| Vehicle motion and vibration | Develop a stable mounting arrangement and investigate motion-related measurement changes. | Compare stationary and controlled-motion test results. |
| Poor data quality | Validate incoming readings and classify missing, stale, or invalid data as `UNKNOWN`. | Inject invalid inputs and verify status handling. |
| False positives and missed hazards | Develop and refine classification criteria using labelled test data. | Measure false-positive and missed-hazard rates across test scenarios. |
| Water, mud, and vibration exposure | Design suitable enclosure and mounting protection. | Inspect and test the assembly under controlled exposure conditions. |
| Excessive warning latency | Optimise local processing and keep the warning path independent of network availability. | Measure end-to-end sensor-to-warning latency on the Raspberry Pi. |

## 2. Priority Risk: Sensor Feasibility

The first priority is determining whether the proposed sensing arrangement can produce useful, repeatable measurements of submerged-road irregularities.

The team will compare sensor-derived measurements against known road profiles under controlled water conditions.

If the sensing arrangement cannot provide reliable evidence, the limitation will be documented and the sensing approach reconsidered before committing to full fabrication.

## 3. Safety Principle

`UNKNOWN` must never be treated as `NORMAL`.

When data is missing, invalid, or insufficient, the system should represent uncertainty rather than issue an unsupported safe-road assessment.

## 4. Current Status

All mitigations are proposed. Their effectiveness remains unverified until supported by documented test results.
