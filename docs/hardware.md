# RoadSight — Hardware Design

**Project:** RoadSight — See Beyond the Water  

## 1. Project Overview

RoadSight is a proposed vehicle-mounted system designed to identify potentially hazardous road irregularities concealed beneath water-covered road surfaces and provide timely warnings to drivers.

The hardware system is designed around an edge-computing unit that collects sensor measurements, processes the available information, and supports local driver alerts.

The primary hardware objective is to investigate whether the selected sensing arrangement can provide useful and repeatable measurements of submerged-road irregularities under controlled conditions.

**Important limitation:** The ability of the selected sensing arrangement to detect road irregularities through water has not yet been established. Sensor feasibility must be verified experimentally before detection performance can be claimed.

## 2. Hardware Design Objectives

The hardware design aims to:

- Collect measurements relevant to submerged-road surface conditions.
- Support local data acquisition and processing inside the vehicle.
- Provide the interfaces required for sensor integration.
- Support driver warnings without depending on an internet connection.
- Record sensor data for testing, analysis, and future improvements.
- Accommodate sensor mounting, vibration, environmental exposure, and power requirements.
- Allow proposed sensors to be changed without redesigning the entire software pipeline.

## 3. Hardware Architecture

The proposed hardware system consists of five functional groups.

### 3.1 Sensing Layer

The sensing layer collects information about the road surface, surrounding water conditions, vehicle motion, and location.

The current design identifies a time-of-flight distance sensor and a camera as the principal selected components. Additional sensing components remain under consideration.

### 3.2 Edge-Computing Unit

The Raspberry Pi 4B acts as the central computing unit.

Its intended responsibilities include:

- Acquiring sensor measurements.
- Managing sensor data and timestamps.
- Supporting the processing and detection pipeline.
- Logging measurements and detected events.
- Generating local warning commands.
- Communicating with the backend when connectivity is available.

### 3.3 Driver Warning Interface

The proposed warning interface may use LEDs, a buzzer, or a display to communicate the system state to the driver.

The final indicators and their electrical interfaces remain to be selected and tested.

### 3.4 Power System

The power system must supply the computing unit and connected sensors within their specified electrical limits.

The final power source, voltage regulation, current capacity, protection, and shutdown arrangement must be determined before physical integration.

### 3.5 Mounting and Enclosure

The mechanical arrangement must hold the sensors in a stable position relative to the vehicle and road.

The design must consider mounting rigidity, sensor alignment, vibration, water exposure, cable routing, and ease of maintenance.

---

## 4. Bill of Materials — Preliminary

The following table records the components identified in the current software architecture. It is not a finalized purchasing list.

| No. | Component | Status | Intended Function |
|---|---|---|---|
| 1 | Raspberry Pi 4B | Confirmed | Edge computing, data acquisition, processing, and logging |
| 2 | VL53L1X Time-of-Flight sensor | Confirmed | Candidate road-profile distance measurement |
| 3 | Arducam NoIR camera — exact model TBD | Confirmed | Ground-truth video and visual context |
| 4 | Water-surface sensor | Proposed | Water presence and depth estimation |
| 5 | Motion sensor / IMU | Proposed | Vehicle vibration and motion measurements |
| 6 | Location sensor / GPS | Proposed | Event location and time reference |
| 7 | Speed or distance sensor | Proposed | Distance-based measurement windows |
| 8 | Driver indicators — LEDs, buzzer, or display | Proposed | Local driver warnings |
| 9 | Power supply and regulation components | To be finalized | Safe and stable power delivery |
| 10 | Mounting bracket and enclosure | To be designed | Mechanical installation and environmental protection |
| 11 | Cables and connectors | To be finalized | Electrical connections between components |

**Cost status:** Component prices, quantities, and the total prototype cost must be added after the bill of materials is verified.

**Sensor feasibility note:** The VL53L1X is currently a candidate for road-profile measurements. Its suitability for detecting submerged-road irregularities must not be assumed until controlled testing is completed.

---

## 5. Sensor Interfaces

The proposed interfaces follow the current system architecture.

| Component | Planned Interface | Data or Function |
|---|---|---|
| VL53L1X ToF sensor | I²C | Distance measurements and sensor status |
| Arducam NoIR camera | CSI | Video frames for visual context and ground-truth recording |
| Water-surface sensor | TBD | Water-related measurements |
| Motion sensor / IMU | I²C or SPI — TBD | Acceleration and angular-rate measurements |
| Location sensor / GPS | UART or USB — TBD | Position, time, and fix-quality information |
| Speed or distance sensor | GPIO or another suitable interface — TBD | Speed or distance information |
| Driver indicators | GPIO — TBD | Warning and status outputs |

The final interfaces, pin assignments, wiring, electrical levels, and data rates must be confirmed against the selected component specifications before connecting the hardware.

## 6. Mechanical Design Considerations

The mounting system must maintain the intended sensor orientation during vehicle movement.

The mechanical design will consider:

- Sensor position relative to the road and vehicle.
- Mounting height and orientation.
- Rigidity and resistance to vibration.
- Protection from splashes, mud, and environmental exposure.
- Protection of cables and connectors.
- Access for maintenance and sensor replacement.
- Compatibility with the selected vehicle or test rig.

The final mounting dimensions and fabrication method will be recorded after the mechanical design is developed.

No mounting dimensions or fabrication specifications are considered finalized at this stage.

## 7. Power and Electrical Safety

The hardware must operate within the voltage and current requirements specified for each component.

Before integration, the team will:

1. Verify the power requirements of the Raspberry Pi and each sensor.
2. Determine the required regulated supply voltages and current capacity.
3. Check connector polarity and common-ground requirements where applicable.
4. Plan cable routing and strain relief.
5. Evaluate protection against short circuits and accidental disconnection.
6. Plan safe shutdown and protection against unexpected power loss.
7. Measure actual power consumption during system operation.

The power architecture remains subject to component selection and bench testing.

## 8. Sensor Feasibility and Validation Plan

Sensor feasibility is the first major hardware validation priority.

The test plan will compare sensor-derived measurements with known road-profile conditions under controlled water conditions.

### Proposed Test Sequence

**Test 1 — Basic sensor operation**
- Confirm that the sensor initializes correctly.
- Record measurements from known reference surfaces.
- Check measurement stability and invalid-reading behaviour.

**Test 2 — Controlled water conditions**
- Repeat measurements under controlled water conditions.
- Compare the results with the known reference profiles.
- Record water conditions and any measurement failures.

**Test 3 — Repeatability**
- Repeat each test condition.
- Compare readings across repeated trials.
- Identify conditions where measurements become unreliable.

**Test 4 — Motion and vibration**
- After safe bench testing, evaluate the effect of controlled movement and vibration.
- Compare stationary and moving measurements.

**Test 5 — Integrated prototype**
- Integrate the selected components only after individual sensor behaviour is understood.
- Measure data quality and sensor-to-warning latency.
- Document false positives and missed hazards using labelled test scenarios.

These tests are planned activities, not completed experiments. Numerical acceptance thresholds will be defined using the test results and project requirements.

## 9. Hardware Risks and Mitigation

| Risk | Proposed Mitigation |
|---|---|
| Unreliable measurements under water | Conduct controlled sensor feasibility tests before committing to the final sensing arrangement. |
| Water-surface interference | Evaluate performance at different water depths and surface conditions. |
| Vehicle vibration | Develop a stable mounting arrangement and test measurement changes under controlled movement. |
| Water or mud exposure | Design appropriate enclosure protection and verify it through testing. |
| Unstable power | Verify supply requirements and measure voltage stability under load. |
| Sensor disconnection or invalid readings | Implement sensor-status checks and ensure failures are reported to the software. |
| Excessive system latency | Measure end-to-end sensor-to-warning latency on the integrated prototype. |
| Unproven detection performance | Document limitations and revise the sensing approach if feasibility tests are unsuccessful. |

## 10. Current Status and Pending Work

The hardware design is at the documentation and planning stage.

### Identified in the Current Architecture
- Raspberry Pi 4B as the edge-computing unit.
- VL53L1X ToF sensor as a candidate distance-measurement input.
- Arducam NoIR camera for video and visual context.

### Still to Be Finalized
- Exact camera model.
- Selection of additional sensors.
- Electrical wiring and pin assignments.
- Power supply and regulation design.
- Mechanical mounting and enclosure.
- Final bill of materials and component costs.
- Hardware integration and sensor feasibility results.

### Completion Criteria

The hardware design will be considered ready for integrated prototype testing when:

- Selected components and their specifications are documented.
- Electrical interfaces and power requirements are verified.
- The mounting arrangement is defined.
- Individual sensor drivers produce valid, timestamped measurements.
- Controlled tests establish whether the selected sensing arrangement provides useful evidence of submerged-road irregularities.

## 11. Safety and Design Principle

RoadSight is intended as an advisory system, not a replacement for driver judgement.

The hardware and software must communicate uncertainty honestly. If required sensor data is missing, invalid, or insufficient, the system must not treat the road as confirmed safe.

**`UNKNOWN` must never be treated as `NORMAL`.**

## 12. References to Related Documentation

- [`software_architecture.md`](software_architecture.md) — Software components, interfaces, and integration.
- [`data_architecture.md`](data_architecture.md) — Sensor-data structures and records.
- [`data_processing_and_detection.md`](data_processing_and_detection.md) — Data-processing and detection pipeline.
- [`potential_solutions_and_risk_mitigation.md`](potential_solutions_and_risk_mitigation.md) — Proposed risk mitigations.

---

**Document status:** Design-stage documentation. Hardware feasibility, integrated operation, and detection performance remain to be demonstrated through testing.
