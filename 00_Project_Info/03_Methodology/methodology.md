# Methodology - Five-Stage Workflow

**Project:** Energy retrofit analysis of a 1965 multifamily residential building (MFH), Frankfurt, Germany  
**Reference typology:** TABULA DE.N.MFH.05.Gen.ReEx.001  
**Current status:** Existing-building baseline validated; retrofit development ongoing.

## 1. Climate Analysis

**Status: Complete**

Frankfurt climate conditions were assessed using Climate Consultant and the Frankfurt IWEC weather file.

The analysis includes:

- Sun-path analysis
- Psychrometric chart
- Wind rose
- Heating and cooling degree-day review

These outputs provide the climatic basis for subsequent building-performance and retrofit decisions.

## 2. Summer Radiation and Overheating Assessment

**Status: Pending**

Solar exposure and potential summer overheating risk of the existing envelope will be assessed using the climate information established in Stage 1.

## 3. Thermal-Bridge Analysis

**Status: Complete**

Five representative junctions of the existing 1965 building were modelled in THERM 7.8 following EN ISO 10211 principles:

1. Roof–Wall Edge
2. Window Jamb
3. Ground Floor–Wall Edge
4. Entrance Door Threshold
5. Balcony Cantilever

Calculated linear thermal transmittance values:

| Junction | Ψ-value |
|---|---:|
| Roof–Wall Edge | 0.624 W/m·K |
| Window Jamb | 0.235 W/m·K |
| Ground Floor–Wall Edge | 0.351 W/m·K |
| Entrance Door Threshold | 0.049 W/m·K |
| Balcony Cantilever | 0.306 W/m·K |

Geometry, boundary conditions, energy-balance checks and detailed results are documented in the project validation record.

## 4. Moisture and Condensation Assessment

**Status: Pending**

Envelope assemblies will be assessed for moisture and condensation risk.

Planned work includes:

- Glaser-method assessment of envelope assemblies
- Interior surface-temperature review at critical junctions
- Identification of potential mould-risk locations

The balcony cantilever junction is expected to require particular attention because of its low interior surface temperature.

## 5. Whole-Building Energy Modelling and Retrofit Comparison

### Existing-Building Baseline

**Status: Complete**

The existing building was modelled in DesignBuilder / EnergyPlus and compared with the TABULA reference typology.

Three simulation runs were used during baseline development:

| Run | Configuration | Heating Demand | Status |
|---|---|---:|---|
| Run01 | Initial intermittent heating schedule | 76.7 kWh/m²·a | Not validated |
| Run02 | Continuous heating, default thermal bridges | 122.8 kWh/m²·a | Validated baseline |
| Run03 | Continuous heating with calculated thermal bridges | 134.3 kWh/m²·a | Current baseline |

Introducing the calculated thermal-bridge values increased simulated heating demand by approximately **9.4%** relative to Run02.

### Retrofit Model

**Status: Pending**

The validated existing-building model will form the basis for the retrofit simulation.

Only renovation-related variables will be changed between the baseline and retrofit cases so that the comparison remains consistent.

## Modelling Conventions

- Climate data, occupancy assumptions, setpoints and schedules are held constant when comparing baseline and retrofit models.
- U-value comparisons identify the relevant surface-film convention where required.
- THERM-derived Ψ-values are used in DesignBuilder where corresponding linear thermal-bridge inputs are available.
- Geometry-based technical outputs are kept separate from conceptual architectural visualisations.
- Only completed and documented results are presented as validated project findings.
