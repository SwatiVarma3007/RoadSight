# RoadSight — Data Architecture



## 1. Overview

RoadSight is a proposed vehicle-mounted system designed to identify potentially hazardous road-surface irregularities concealed by water.

The data architecture describes how sensor data is acquired, validated, processed, classified, and recorded. Core processing and warning decisions are intended to operate locally without continuous network connectivity.

## 2. Proposed Components

| Component | Responsibility |
|---|---|
| Raspberry Pi Camera Module 3 | Captures road and projected laser-line images. |
| 650 nm line laser | Projects a line onto the road surface for optical profiling. |
| ESP32 DevKit V1 | Coordinates sensor acquisition. |
| MPU6050 IMU | Provides vehicle-motion measurements. |
| NEO-6M GPS | Provides location and available positioning information. |
| Raspberry Pi 5 (4 GB) | Performs local processing, classification, and event logging. |

*The proposed hardware configuration remains subject to implementation and testing.*

## 3. Data Processing Pipeline

1. **Data Acquisition:** Collect camera frames and available sensor readings with timestamps and source identifiers.
2. **Input Validation:** Check for missing, stale, malformed, or invalid data.
3. **Synchronization:** Align measurements from different sensors where appropriate.
4. **Preprocessing:** Handle noise and outliers without concealing unreliable measurements.
5. **Feature Extraction:** Prepare road-profile, visual, vehicle-motion, and location features.
6. **Hazard Detection:** Apply the proposed rule-based detection logic. Lightweight machine learning may be considered later if required.
7. **Classification:** Assign a hazard state based on available evidence and defined criteria.
8. **Warning and Logging:** Generate an appropriate driver indication and record relevant event information locally.

If the input data is insufficient or unreliable, the system should use the `UNKNOWN` state rather than infer that the road is safe.

## 4. Hazard Classification

| State | Meaning |
|---|---|
| `NORMAL` | No hazard detected by the available checks; this does not guarantee a hazard-free road. |
| `POSSIBLE_HAZARD` | Evidence suggests a potential road irregularity. |
| `HAZARD` | Defined hazard-detection criteria have been met. |
| `UNKNOWN` | Data is missing, invalid, stale, or insufficient for reliable assessment. |

Classification thresholds and state-transition rules remain to be implemented and validated.

## 5. Event Logging

Each event record may contain:

- Timestamp and event identifier.
- Hazard classification.
- GPS location, if available and valid.
- Relevant sensor measurements or feature summaries.
- Data-quality status.
- Warning action, where applicable.

The local event log supports testing, debugging, and future development of location-tagged hazard records.

## 6. Data Quality and Failure Handling

| Condition | Proposed response |
|---|---|
| Missing or invalid sensor data | Reject or flag the input. |
| Stale or unsynchronized measurements | Avoid unreliable sensor fusion. |
| Excessive noise or inconsistent readings | Flag the data and apply appropriate validated checks. |
| Unavailable GPS | Mark location as unavailable or uncertain. |
| Insufficient evidence | Set the classification to `UNKNOWN`. |
| Network unavailable | Continue local processing if required hardware and sensor inputs remain operational. |

## 7. Through-Water Feasibility

Accurate road-profile measurement through water is a critical unverified capability. Refraction, scattering, and reflections may distort or weaken the observed laser line.

The proposed validation process is to:

1. Establish a reference profile on a known surface.
2. Test surfaces with independently measured depressions.
3. Repeat measurements under controlled water conditions.
4. Compare estimated profiles against reference measurements.
5. Evaluate measurement error, repeatability, and valid-observation rate.
6. Decide whether to continue, restrict operating conditions, or use the fallback approach.

**No successful through-water measurement performance is claimed at this stage.**

If through-water profiling proves unsuitable, the proposed fallback is to prioritise dry-road profiling, identify potentially water-covered road stretches where feasible, and use stored hazard information with vehicle-motion context where appropriate.

## 8. Validation Plan

| Area | Evaluation |
|---|---|
| Sensor acquisition | Verify usable readings and image capture. |
| Data validation | Test missing, stale, and invalid inputs. |
| Synchronization | Evaluate timestamp alignment. |
| Road-profile estimation | Compare estimates with reference measurements. |
| Through-water profiling | Conduct controlled feasibility experiments. |
| Hazard classification | Evaluate states against labelled test scenarios. |
| Event logging | Verify timestamps, classifications, and location records. |
| Offline operation | Test local processing without continuous internet access. |

Performance thresholds and acceptance criteria must be defined before testing. Results will be documented after experiments are completed.

## 9. Current Status

- System concept and proposed architecture: defined.
- Hardware configuration: proposed.
- Processing and classification pipeline: proposed.
- Through-water profiling: pending feasibility testing.
- Detection thresholds and performance: pending validation.
- Integrated prototype: implementation pending.

## 10. Design Principle

RoadSight aims to convert road-surface observations and vehicle context into a cautious, location-aware hazard assessment. The architecture prioritises data quality, local processing, explicit uncertainty handling, and measurable validation.
