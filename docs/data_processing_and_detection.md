# RoadSight — Data Detection and processing 


## 1. Objective

The proposed detection pipeline identifies potentially hazardous road-surface irregularities using camera observations, laser-derived road-profile measurements, vehicle-motion context, and location information.

The system classifies observations into `NORMAL`, `POSSIBLE_HAZARD`, `HAZARD`, or `UNKNOWN`. Detection performance, thresholds, and through-water measurement capability remain unvalidated.

## 2. Detection Inputs

| Input | Purpose |
|---|---|
| Camera frames | Observe the road surface and projected laser line. |
| Laser-derived measurements | Estimate road-profile features, subject to calibration and measurement feasibility. |
| IMU readings | Provide vehicle-motion context to help interpret measurements. |
| GPS data | Associate detected events with location when valid positioning is available. |
| Data-quality indicators | Determine whether the available measurements are suitable for assessment. |

## 3. Detection Pipeline

### Step 1: Input Validation
Check sensor readings and image frames for missing data, invalid values, stale timestamps, and acquisition errors.

If the required evidence is insufficient, return `UNKNOWN`.

### Step 2: Preprocessing
Synchronize relevant measurements and apply suitable noise filtering and outlier handling. Unreliable observations must not be treated as valid road measurements.

### Step 3: Feature Extraction
Prepare relevant features, which may include:

- Laser-line position and displacement.
- Estimated road-profile changes.
- Visual road-surface characteristics.
- Vehicle acceleration and angular velocity.
- Location and timestamp information.

The availability and accuracy of these features depend on calibration and testing.

### Step 4: Pattern Analysis
Evaluate the prepared features for patterns that may indicate a road depression or other irregularity.

The initial design proposes rule-based detection. A lightweight machine-learning model may be considered if testing demonstrates a need.

### Step 5: Hazard Classification
Assign a classification according to the available evidence and detection criteria.

| State | Detection interpretation |
|---|---|
| `NORMAL` | No hazard detected by the available checks. |
| `POSSIBLE_HAZARD` | A potential irregularity is indicated, but evidence is inconclusive. |
| `HAZARD` | The defined hazard-detection criteria are met. |
| `UNKNOWN` | Data quality or quantity is insufficient for reliable classification. |

A `NORMAL` result does not guarantee that the road is hazard-free.

### Step 6: Warning and Event Logging
Pass the classification to the proposed warning logic and record relevant event details, including timestamp, available location, classification, and data-quality status.

Warning behaviour and timing remain subject to implementation and validation.

## 4. Through-Water Detection Limitation

The ability to measure road-profile irregularities through water is the principal technical uncertainty.

Water may cause refraction, scattering, reflections, or loss of laser-line visibility. Therefore, dry-road measurement performance cannot be assumed to apply to submerged surfaces.

The proposed validation process will compare estimated profiles against known reference measurements under controlled dry and water-covered conditions.

If reliable through-water profiling cannot be established, the team will evaluate a fallback based on dry-road profiling, identifying potentially water-covered stretches where feasible, and using stored hazard information with vehicle-motion context.

Neither the primary through-water method nor the fallback is claimed to be validated.

## 5. Validation Metrics

The following metrics will be considered during testing:

- **Detection precision:** Proportion of positive hazard detections that are correct.
- **Detection recall:** Proportion of reference hazards that are detected.
- **False-positive rate:** Frequency of incorrect hazard alerts.
- **Measurement error:** Difference between estimated and reference road profiles.
- **Repeatability:** Consistency across repeated measurements.
- **Classification latency:** Time from usable input to classification.
- **UNKNOWN rate:** Frequency with which the system cannot make a reliable assessment.

Acceptance thresholds must be defined before evaluation. Results will be reported only after testing.

## 6. Current Status

- Detection workflow: proposed.
- Input validation and preprocessing: planned.
- Detection rules and thresholds: pending implementation.
- Hazard classification: proposed.
- Through-water profiling: pending controlled feasibility testing.
- Detection accuracy and latency: not yet established.

## 7. Design Principle

RoadSight detection is designed to prioritise reliable evidence over forced classification. When measurements are missing, inconsistent, or insufficient, the system should represent uncertainty explicitly rather than issue an unsupported confident assessment.
