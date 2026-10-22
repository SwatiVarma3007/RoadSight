# RoadSight — Technical Challenges and Risks

**Status:** Anticipated engineering risks; not yet confirmed through testing.

| Challenge | Potential impact | What needs to be investigated |
|---|---|---|
| Submerged-road sensing feasibility | Road irregularities may not be distinguishable beneath water. | Test whether the selected VL53L1X ToF sensor and Arducam NoIR camera provide useful measurements under controlled conditions. |
| Water-surface interference | Reflections, movement and water conditions may distort measurements. | Compare readings across controlled water depths and surface conditions. |
| Vehicle motion and vibration | Sensor movement may be mistaken for a road irregularity. | Evaluate mounting stability and the effect of movement during testing. |
| Sensor variability and data quality | Inconsistent, missing or unreliable readings may affect classification. | Implement data-quality checks and handle insufficient data as `UNKNOWN`. |
| False positives and missed hazards | Incorrect classification may cause unnecessary warnings or fail to identify a hazard. | Test against controlled road profiles and labelled test scenarios. |
| Environmental exposure | Water, mud, splashes and vibration may affect hardware reliability. | Evaluate enclosure, mounting and protection requirements before vehicle-mounted testing. |
| Real-time processing and warning delay | Delayed processing may make warnings less useful. | Measure end-to-end processing and warning latency on the Raspberry Pi 4 Model B. |

## Risk Priorities

1. **Highest priority:** Establish sensor feasibility before committing to full fabrication.
2. **High priority:** Verify data quality and distinguish hazard states from uncertain readings.
3. **Integration priority:** Assess environmental protection, mounting stability and processing latency.

**Important:** These are anticipated risks, not verified failures. Mitigations and design decisions should be updated as experimental evidence becomes available. Do not claim validated detection performance before controlled testing.
