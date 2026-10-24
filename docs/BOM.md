# RoadSight — Bill of Materials (BOM)



## 1. Purpose

This document lists the hardware components required for the proposed RoadSight prototype. It records each component's intended function, quantity, procurement status, and cost.

The bill of materials will be updated as component selection, purchasing, and hardware testing progress.

## 2. Preliminary Component List

| No. | Component | Quantity | Purpose | Selection Status | Unit Cost (₹) | Total Cost (₹) |
|---|---|---:|---|---|---:|---:|
| 1 | Raspberry Pi 4B | 1 | Edge computing and local processing | Confirmed | TBD | TBD |
| 2 | VL53L1X ToF sensor | 1 | Candidate road-profile distance measurement | Confirmed | TBD | TBD |
| 3 | Arducam NoIR camera | 1 | Video recording and visual context | Confirmed; exact model TBD | TBD | TBD |
| 4 | Water-surface sensor | TBD | Water presence and depth estimation | Proposed | TBD | TBD |
| 5 | Motion sensor / IMU | 1 | Vehicle motion and vibration measurements | Proposed | TBD | TBD |
| 6 | GPS / location sensor | 1 | Event location and time reference | Proposed | TBD | TBD |
| 7 | Speed / distance sensor | TBD | Distance-based measurement windows | Proposed | TBD | TBD |
| 8 | Driver warning indicators | TBD | Visual or audible warnings | Proposed | TBD | TBD |
| 9 | Power supply and regulation components | TBD | Power delivery to the computing unit and sensors | To be finalized | TBD | TBD |
| 10 | Mounting bracket and enclosure | TBD | Sensor mounting and environmental protection | To be designed | TBD | TBD |
| 11 | Cables and connectors | TBD | Electrical connections | To be finalized | TBD | TBD |
| 12 | Miscellaneous hardware | TBD | Fasteners and assembly materials | To be finalized | TBD | TBD |

**Note:** Quantities marked `TBD` must be finalized during detailed design. Costs are intentionally left unfilled until verified quotations or purchase prices are available.

## 3. Cost Calculation

For each component:

**Line-item cost = Quantity × Unit cost**

**Total prototype cost = Sum of all line-item costs**

The final budget should also account for shipping, taxes, spare components, fabrication, and any required tools or adapters.

## 4. Procurement Status

Use the following statuses to track purchasing:

- `Not researched` — specifications and suppliers have not been evaluated.
- `To purchase` — selected but not yet purchased.
- `Ordered` — purchase placed.
- `Received` — component received.
- `Tested` — component has passed its individual bench test.
- `Rejected` — unsuitable for the project after evaluation.

Update each component's status as procurement progresses.

## 5. Important Hardware Considerations

1. Verify the electrical specifications of every component before purchasing or connecting it.
2. Confirm compatibility with the Raspberry Pi 4B and the intended interfaces.
3. Evaluate the VL53L1X under controlled water conditions before relying on it for submerged-road detection.
4. Select the final camera model and confirm its compatibility with the computing unit.
5. Finalize power requirements after the component list is confirmed.
6. Avoid purchasing optional sensors until their role and feasibility have been evaluated.

## 6. Pending Decisions

- Exact Arducam NoIR camera model.
- Selection and specifications of additional sensors.
- Final warning-indicator arrangement.
- Power supply and voltage-regulation design.
- Mounting and enclosure materials.
- Verified supplier prices and total prototype budget.

## 7. Revision History

| Version | Status | Description |
|---|---|---|
| 0.1 | Preliminary | Initial component list for the design-stage prototype |

---

**Document status:** Preliminary bill of materials. Component costs, quantities, and final selections must be verified before procurement.
