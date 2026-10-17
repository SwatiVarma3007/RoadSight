RoadSight Data Architecture

Document Information

Details

Document

docs/data_architecture.md

Version

v1.0-draft

Project Phase

Stage 2 — Design Specification

Status

Initial design; hardware-dependent decisions pending confirmation

Owner

P3 — Data Architecture, Processing and Detection

Review

P1 — Embedded Systems; P2 — Mechanical Design; P4 — Software and Integration

Design-status note: This document describes the proposed data architecture for RoadSight. Hardware-dependent parameters, sampling rates, processing windows, detection thresholds and performance targets remain subject to confirmation and experimental validation. No real-road dataset or validated detection-performance result is claimed at this stage.

1. Purpose and Scope

RoadSight is a proposed vehicle-mounted multi-sensor system designed to identify potentially hazardous submerged-road conditions and provide timely warnings to drivers.

Water-covered roads can conceal potholes, depressions and other surface irregularities. The system will use sensor measurements and contextual information, such as vehicle motion and speed, to assess potentially hazardous changes in the submerged road surface or profile.

This document defines:

The proposed flow of data through RoadSight.

The information required from sensors and the experimental setup.

The planned data format and data-quality requirements.

The proposed data-processing and detection workflow.

The ground-truth labelling and evaluation approach.

The technical decisions that must be confirmed during implementation and testing.

The architecture is a design specification, not a claim that all proposed components or functions have been implemented.

2. Detection Scope

RoadSight focuses on identifying potentially hazardous changes in submerged-road surface/profile conditions using sensor measurements and available contextual information.

2.1 Detection Classes

Class

Meaning

Proposed system response

NORMAL

Measurements do not indicate a significant hazardous irregularity.

No hazard warning.

POSSIBLE HAZARD

Measurements indicate an unusual or uncertain pattern that requires caution.

Caution indication.

HAZARD

Measurements meet hazard criteria established through controlled experiments.

Hazard warning.

A separate internal data-quality or system state, UNKNOWN, may be used when measurements are missing, invalid, stale or insufficient for a reliable assessment. UNKNOWN is not a fourth hazard class and must never be interpreted as NORMAL.

The criteria and thresholds for these states will be determined and evaluated using controlled experimental observations.

2.2 Out of Scope

The current design does not target:

Flood or weather prediction.

Traffic or pedestrian detection.

General road-quality assessment.

Guaranteed detection of every submerged road hazard.

A vehicle-to-vehicle hazard-sharing network as a core requirement.

Any additional networking or cloud functionality will be considered separately if it is justified by the final requirements and available implementation resources.

3. Proposed End-to-End Data Flow

The planned processing sequence is:

Sensor measurements and vehicle context
→ Data acquisition
→ Timestamping and experiment identification
→ Data validation
→ Synchronization
→ Preprocessing and noise handling
→ Windowing and feature extraction
→ Detection methodology
→ Hazard classification
→ Driver warning and event logging

Ground-truth labels collected during controlled experiments will be maintained separately from detector predictions. This separation is necessary for an independent evaluation of the detection methodology.

3.1 Functional Components

Component

Responsibility

Status

Sensor acquisition

Collect measurements from the selected sensing hardware.

Hardware-dependent

Data logging

Record measurements and identify each experiment.

Planned

Data validation

Identify missing, invalid or implausible measurements.

Planned

Synchronization

Align measurements from different sources where required.

Planned

Preprocessing

Handle noise, outliers and invalid samples.

Planned

Feature extraction

Calculate useful characteristics from measurement data.

Planned

Detection

Assess measurements using an initial rule-based baseline.

Planned

Classification

Assign NORMAL, POSSIBLE HAZARD or HAZARD when evidence is sufficient.

Planned

Warning interface

Communicate the resulting state to the driver.

P4-led integration

Evaluation

Compare detector outputs with ground-truth labels.

Planned for controlled testing

The exact implementation and interfaces will be finalized after the team confirms the hardware and software design.

4. Data Sources and Acquisition

The data architecture must support measurements from the selected road-sensing hardware and any contextual sensors included in the final system.

Data category

Required information

Source or method

Status

Road-sensing measurements

Raw readings used to infer submerged-road surface/profile changes.

Selected road-sensing hardware

Sensor selection/interface to confirm

Vehicle motion

Relevant motion measurements, such as acceleration or angular rate, if an IMU is included.

IMU or selected equivalent

To confirm

Vehicle speed

Speed or an appropriate speed estimate.

Selected speed-measurement method

To confirm

Position

Latitude and longitude when location is available and required.

GPS/GNSS, if included

To confirm

Water conditions

Water depth or other controlled water-condition measurements needed for testing.

Experimental measurement method

Protocol to define

Road-condition reference

Known surface irregularity and physical characteristics used during testing.

Controlled test setup and direct measurement

Protocol to define

Ground-truth label

Reference hazard class for an experiment or test segment.

Documented labelling procedure

To define before evaluation

System status

Data availability, sensor health and relevant error indicators.

Acquisition and software components

Planned

Only fields supported by the final hardware configuration will be included in the implemented schema. Unavailable measurements will be represented explicitly rather than fabricated or inferred without a documented method.

5. Proposed Data Schema

The following fields form the initial logical schema for experiment-level records or synchronized analysis records. The final physical file format may differ between raw sensor logs and processed data.

Field

Data type

Description

experiment_id

String

Unique identifier for a controlled test run.

timestamp

Timestamp or numeric time value

Time associated with a measurement, using the acquisition system's documented convention.

source

String

Data provenance, such as sim, bench or road.

sensor_readings

Numeric values or structured fields

Measurements from the selected road-sensing hardware.

vehicle_motion

Numeric values or structured fields

Available motion measurements, if supported by the final configuration.

vehicle_speed

Numeric value or null

Measured or estimated speed, with its source and unit documented.

gps_lat

Numeric value or null

Latitude, if location data is available.

gps_lon

Numeric value or null

Longitude, if location data is available.

water_depth

Numeric value or null

Water depth measured using the defined experimental method, where applicable.

road_condition

String or structured reference

Known physical condition used in the experiment.

ground_truth_label

String or null

Reference class assigned using the documented labelling procedure.

data_quality

String or structured flags

Indicates whether the measurement is valid, degraded or unavailable.

The schema will be refined when the sensor interfaces, measurement units, sampling characteristics and experiment protocol are confirmed.

Raw sensor streams may require separate files because different sensors can produce different numbers of readings over the same experiment. Processed records will reference the corresponding experiment and time or analysis window.

6. Data Processing Pipeline

6.1 Data Validation

The validation stage will check:

Whether required fields are present.

Whether timestamps and experiment identifiers are valid.

Whether numeric values fall within documented sensor or physical ranges.

Whether measurements are missing, repeated unexpectedly or stale.

Whether the data source and measurement units are documented.

Invalid records will be flagged and handled according to the processing rules. Missing measurements must not be interpreted as evidence that the road is safe.

6.2 Synchronization

Measurements from different sensors may be collected at different rates. Where multiple streams are used together, their timestamps and acquisition conventions must be documented.

The synchronization stage will align measurements using an appropriate method determined by the final hardware and data rates. Interpolated or resampled values, if used, will be distinguishable from directly measured values.

The clock source, timestamp resolution and synchronization method remain implementation decisions.

6.3 Preprocessing

Potential preprocessing operations include:

Noise reduction using suitable filters.

Identification and handling of outliers.

Detection of invalid or stale measurements.

Calibration or coordinate correction where required.

Preservation of the original raw measurements for traceability.

Filtering methods and parameters will be selected based on sensor characteristics and observed experimental data. No filter configuration is considered validated at this stage.

6.4 Windowing and Feature Extraction

After validation and synchronization, measurements may be grouped into time-based or distance-based windows, depending on the final measurement setup.

Candidate features may include:

Minimum, maximum and range of relevant road-profile measurements.

Changes in measurements between consecutive samples.

Variation in sensor readings within a window.

Relevant vehicle-motion characteristics.

Data-validity or measurement-coverage indicators.

The final features and window parameters will be selected based on their physical relevance, sensor capabilities and experimental observations.

6.5 Detection Methodology

The initial approach will be a rule-based baseline detector. Its purpose is to establish a simple, explainable reference before considering more complex methods.

The proposed workflow is:

Inspect and understand the collected measurements.

Establish the ground-truth labelling procedure.

Identify candidate features associated with the tested road conditions.

Develop and document baseline detection rules.

Compare predicted classes with ground-truth labels.

Evaluate missed hazards, false warnings and overall classification performance.

Consider lightweight machine learning only if the available dataset and baseline results justify it.

Detection thresholds will not be selected arbitrarily or presented as experimentally established before testing.

7. Ground Truth and Experimental Labelling

Ground-truth labels provide the reference against which detector predictions will be evaluated.

The experimental protocol must document the physical road condition, relevant water conditions, measurement method and reference class for each test or test segment.

Where applicable, reference measurements may include:

Presence or absence of a surface irregularity.

Measured dimensions of the irregularity.

Water depth.

Test conditions and measurement limitations.

The team will define the physical criteria for assigning NORMAL, POSSIBLE HAZARD and HAZARD before evaluating detector performance. The criteria must be documented independently of the detector's own predictions.

Ground-truth labels will be stored separately from sensor predictions to avoid circular evaluation.

The detailed procedure, test repetitions and acceptance criteria will be documented in docs/experiment_protocol.md before formal validation.

8. Data Quality and Failure Handling

Condition

Proposed handling

Missing measurement

Mark the measurement as missing and determine whether the affected analysis can continue.

Invalid or implausible value

Flag the value and exclude it from calculations where required.

Stale sensor data

Flag the data and assess whether the system has sufficient valid information to classify the condition.

Unsynchronized streams

Mark the affected records or windows as unsuitable for combined analysis until alignment is resolved.

Sensor or communication failure

Record the fault and use an appropriate system-status response.

Insufficient valid data

Report an internal UNKNOWN or invalid-data state rather than treating the road as safe.

Corrupted experiment file

Preserve the original file where possible, document the issue and exclude affected records from analysis when necessary.

Simulated data

Keep its provenance explicit and separate it from measured experimental data in reported results.

The final failure-handling behaviour must be tested against the actual hardware and software interfaces.

9. Data Provenance and Version Control

Every dataset used for analysis must have documented provenance.

The following principles will apply:

Distinguish simulated, bench-test and real-road measurements.

Preserve raw measurements separately from processed outputs.

Record experiment conditions and relevant measurement units.

Document preprocessing and feature-extraction changes.

Record the data-schema version and processing-code version used for analysis.

Maintain a clear record of excluded data and the reason for exclusion.

Never report simulated results as evidence of real-road performance.

Do not claim detection accuracy or system reliability without appropriate experimental evidence.

Schema changes will be documented in this file and reflected in the corresponding code and data dictionary.

10. Data Storage and Software Interfaces

During the design stage, CSV files are proposed for small experimental datasets because they are readable and easy to inspect.

The implementation may use separate files for raw sensor streams, experiment metadata, ground-truth labels and processed features. The final file organization will depend on the sensor configuration and acquisition software.

The proposed logical software interfaces are:

Acquisition to logging: measurements, timestamps and source information.

Logging to processing: recorded data with documented fields and units.

Processing to detection: validated measurements and extracted features.

Detection to warning logic: predicted class and relevant system/data-quality status.

Processing to evaluation: predictions, ground-truth labels and evaluation records.

The physical communication protocols, storage hardware, backend technology and dashboard interface are not finalized by this document. They will be documented separately if adopted by the team.

11. Evaluation Plan

The detection methodology will be evaluated using controlled test observations and independently assigned ground-truth labels.

Planned evaluation measures include:

Metric

Purpose

Precision

Measures how many predicted hazards are actually labelled as hazards.

Recall

Measures how many labelled hazards are detected.

F1-score

Summarizes the balance between precision and recall.

False-positive count or rate

Measures unnecessary hazard warnings.

False-negative count or rate

Measures missed hazards.

Response latency

Measures the delay between relevant measurements and the corresponding output.

Data-loss rate

Assesses missing or lost measurements during acquisition.

Repeatability

Assesses whether repeated controlled tests produce consistent results.

The suitability of each metric and its calculation method will be documented before evaluation.

No numerical performance result is claimed in this design document. Acceptance targets and test procedures will be established and justified as the design and experimental evidence develop.

12. Privacy and Security

If location data is collected, it will be handled only for the project purposes that require it.

The implementation should:

Avoid storing personal information that is not necessary for testing.

Restrict access to experimental datasets where appropriate.

Avoid committing credentials, passwords, tokens or private keys to the repository.

Document any sharing or publication of location-bearing datasets.

Review applicable privacy and data-protection obligations before collecting or publishing real-world location data.

The precise storage, access-control and data-retention arrangements remain to be defined according to the final implementation.

13. Open Technical Decisions

Decision

Required action

Responsible role

Final sensor selection and interfaces

Confirm selected components and their capabilities.

P1 with P2

Mechanical measurement method

Confirm how submerged-road surface/profile changes will be measured.

P2 with P1

Available contextual measurements

Confirm whether motion, speed and location data will be available.

P1

Timestamp and synchronization method

Define the acquisition-time convention and alignment approach.

P1 and P4

Data schema and units

Finalize fields after sensor interfaces are confirmed.

P3 with P1

Sampling characteristics

Measure or verify achievable acquisition rates.

P1

Experiment conditions and ground truth

Define controlled test conditions and labelling criteria.

P3 with P1 and P2

Windowing and feature set

Select based on the final data and physical relevance.

P3

Detection rules and thresholds

Develop and evaluate using experimental observations.

P3

Warning interface and system integration

Confirm the software interfaces and driver-warning behaviour.

P4 with P1 and P3

Evaluation acceptance targets

Define and justify before formal validation.

Entire team

These decisions will be updated as the team completes design reviews and experiments.

14. Stage 2 Deliverables and Next Steps

The data and software design work will progress through the following deliverables:

This data architecture document.

A versioned data dictionary describing fields, types, units and sources.

An experiment protocol defining controlled conditions and ground-truth labelling.

A CSV template for recording experimental observations.

A preliminary data-validation and analysis script.

A documented processing and detection workflow.

An evidence record distinguishing proposed design, simulation, bench testing and validated measurements.

The immediate next step is to confirm the hardware-dependent data fields with the embedded and mechanical team members, then create the data dictionary and experiment protocol.

15. Changelog

Version

Status

Change

v1.0-draft

Stage 2 design

Defined the proposed data flow, logical schema, processing pipeline, data-quality principles, evaluation approach and pending technical decisions.