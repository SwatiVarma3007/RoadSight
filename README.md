RoadSight

A vehicle-mounted multi-sensor system for identifying potentially hazardous submerged-road conditions and warning drivers.

1. Project Overview

RoadSight aims to help drivers travelling through water-covered roads identify potentially hazardous submerged-road irregularities that may not be visible to the driver.

The proposed system will use sensor measurements and contextual information, such as vehicle motion and speed, to assess submerged-road conditions and provide appropriate warnings.

2. Problem Statement

Water-covered roads can conceal potholes, depressions and other surface irregularities from drivers, increasing the risk of sudden vehicle impact, loss of control and vehicle damage.

3. Project Objectives

Investigate suitable sensing approaches for submerged-road conditions.

Design a structured multi-sensor data acquisition and logging approach.

Develop a data-processing and detection methodology.

Classify observations as NORMAL, POSSIBLE HAZARD or HAZARD.

Design a warning workflow for drivers.

Evaluate the system through controlled experiments.

4. Detection Scope

RoadSight will focus on detecting potentially hazardous changes in submerged road surface/profile using sensor measurements and contextual information such as vehicle motion and speed.

Proposed detection states

NORMAL: No significant hazardous irregularity indicated.

POSSIBLE HAZARD: An unusual or uncertain measurement pattern is observed.

HAZARD: The observed pattern meets experimentally established hazard criteria.

Detection thresholds will be determined through controlled experiments rather than assumed in advance.

5. Software and Data Work

The software/data work is planned to include:

Data schema and data dictionary.

Experiment identification and ground-truth labelling.

Data validation and synchronization.

Signal processing and feature extraction.

Rule-based baseline detection.

Evaluation of lightweight machine learning if justified by experimental results.

Performance evaluation using appropriate metrics.

6. Current Project Status

Phase: Design specification and independent software/data preparation.

Current work includes defining data requirements, planning the processing pipeline and documenting the detection methodology.

Hardware-dependent implementation and performance validation remain pending until the required interfaces and experimental data are available.

7. Repository Structure

docs/ — Technical documentation and design decisions.

data/ — Data schemas, templates and approved experiment records.

src/ — Data-processing and analysis code.

experiments/ — Experimental procedures and results.

evidence/ — Relevant screenshots, diagrams and project evidence.

8. Team Responsibilities

P1: Embedded systems and sensor research.

P2: Mechanical design and AI/ML technical support.

P3: Data architecture, preprocessing, feature engineering and detection evaluation.

P4: Software architecture, dashboard and integration.

9. Project Integrity

RoadSight will distinguish between proposed designs, synthetic data, measured experimental data and validated results. Performance claims will only be reported when supported by appropriate sources, calculations or experiments.

10. Project Status and Updates

This repository will be updated as the design, implementation and validation work progresses.
