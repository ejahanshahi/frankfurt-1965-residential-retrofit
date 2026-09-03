# Frankfurt 1965 Residential Retrofit

**Energy-performance assessment and retrofit study of a 1965 multifamily residential building in Frankfurt, Germany**

This repository documents an ongoing building-performance and retrofit study of a representative 1965 multifamily residential building (MFH) in Frankfurt.

The project combines climate analysis, BIM-based existing-condition modelling, whole-building energy simulation, envelope assessment and two-dimensional thermal-bridge analysis to establish a documented baseline before developing retrofit measures.

**Reference typology:** TABULA `DE.N.MFH.05.Gen.ReEx.001`

---

## Project Overview

- **Location:** Frankfurt, Germany
- **Building type:** Multifamily residential building
- **Construction period:** 1965
- **Footprint:** approximately 16 × 12 m
- **Number of floors:** 4
- **Floor-to-floor height:** approximately 2.75 m
- **Heated floor area:** approximately 768 m²
- **Main façades:** north / south
- **Project status:** Ongoing

The study uses the existing building as a validated baseline for a later baseline-to-retrofit comparison.

GEG requirements and KfW/BEG guidance are used as reference frameworks during retrofit development. No final retrofit-performance claim is made at the current stage.

---

## Research Workflow

The project is structured in five main stages:

1. **Climate analysis**
2. **Summer radiation and overheating assessment**
3. **Thermal-bridge analysis**
4. **Moisture and condensation assessment**
5. **Whole-building energy modelling and retrofit comparison**

Completed analyses and their supporting evidence are progressively documented in this repository.

---

## 1. Climate Analysis

**Status: Complete**

Frankfurt climate conditions were reviewed using Climate Consultant with IWEC weather data.

The documented outputs currently include:

- Weather-data summary
- Sun-path analysis
- Psychrometric chart
- Wind-wheel analysis

Evidence:

[Climate Analysis Evidence](03_Analysis/01_Climate/01_Before_BASELINE/)

The original IWEC weather dataset is not redistributed through this public repository.

---

## 2. Summer Radiation and Overheating Assessment

**Status: Pending**

The next climate-related stage will examine solar exposure and potential summer overheating risk of the existing envelope.

---

## 3. Thermal-Bridge Analysis

**Status: Complete**

Five representative existing-building junctions were modelled in **THERM 7.8** following EN ISO 10211 principles.

| Junction | Calculated Ψ-value |
|---|---:|
| Roof–Wall Edge | 0.624 W/m·K |
| Window Jamb | 0.235 W/m·K |
| Ground Floor–Wall Edge | 0.351 W/m·K |
| Entrance Door Threshold | 0.049 W/m·K |
| Balcony Cantilever | 0.306 W/m·K |

The roof–wall edge produced the highest calculated Ψ-value among the five analysed junctions and represents a significant linear heat-loss path in the existing envelope.

THERM source models:

[THERM Models](02_Models/01_Before_BASELINE/THERM/)

Supporting screenshots:

[THERM Evidence](05_Screenshots/01_Before_BASELINE/THERM/)

---

## 4. Moisture and Condensation Assessment

**Status: Pending**

Planned work includes:

- Glaser-method assessment of envelope assemblies
- Interior surface-temperature review
- Condensation-risk assessment
- Identification of potentially critical mould-risk locations

The balcony cantilever will receive particular attention because of its relatively low interior surface temperature.

---

## 5. Whole-Building Energy Modelling

**Status: Baseline Complete — Retrofit Pending**

The building was modelled in **DesignBuilder / EnergyPlus**.

Three simulation runs were used during baseline development:

| Run | Configuration | Heating Demand | Assessment |
|---|---|---:|---|
| Run01 | Initial intermittent heating schedule | 76.7 kWh/m²·a | Not validated |
| Run02 | Continuous heating, default thermal bridges | 122.8 kWh/m²·a | Validated baseline |
| Run03 | Continuous heating with calculated thermal bridges | 134.3 kWh/m²·a | Current baseline |

Introducing the calculated thermal-bridge values increased simulated heating demand by approximately **9.4%** relative to Run02.

Run03 is therefore used as the current baseline for subsequent retrofit development.

DesignBuilder source model:

[DesignBuilder Baseline Model](02_Models/01_Before_BASELINE/DesignBuilder/)

Simulation evidence:

[DesignBuilder Baseline Evidence](05_Screenshots/01_Before_BASELINE/DesignBuilder/)

---

## Envelope Assessment

Existing wall and window assemblies were also reviewed using **u-wert.net** as part of the envelope-performance assessment.

Evidence:

[Existing Wall U-value](05_Screenshots/01_Before_BASELINE/U-wert.net_Wall/)

[Existing Window U-value](05_Screenshots/01_Before_BASELINE/U-wert.net_Windows/)

---

## BIM Model

The existing-condition building geometry was developed in **Autodesk Revit** and used as the geometric basis for the performance-analysis workflow.

Source files:

[Revit Baseline Model](02_Models/01_Before_BASELINE/Revit/)

---

## Software and Methods

- Autodesk Revit
- DesignBuilder
- EnergyPlus
- THERM 7.8
- Climate Consultant
- u-wert.net
- TABULA building typology data
- EN ISO 10211 principles for two-dimensional thermal-bridge assessment

---

## Repository Documentation

Detailed project documentation is available here:

- [Project Brief and Scope](00_Project_Info/01_Brief_Scope/brief.md)
- [Methodology](00_Project_Info/03_Methodology/methodology.md)
- [Baseline Validation Log](04_Results/01_Before_BASELINE/Validation_Log.md)

The validation log records modelling assumptions, intermediate simulation runs, thermal-bridge calculations and the reasoning used to establish the current baseline.

---

## Current Development

The validated existing-building model will be used for the next stages of the study:

- Moisture and condensation assessment
- Retrofit envelope development
- Updated thermal-bridge assessment
- Retrofit energy simulation
- Baseline-versus-retrofit comparison
- Final technical documentation

Only completed and documented analyses are presented as validated findings.

---

## Repository Purpose

This repository is maintained as a transparent technical record of the research workflow rather than as a complete project archive.

It includes selected source models, calculations, validation records and visual evidence needed to understand and reproduce the main analytical workflow.

Large backups, temporary files, private administrative material and licensed weather datasets are intentionally excluded.
