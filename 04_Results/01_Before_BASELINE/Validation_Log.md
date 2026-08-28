# Validation Log — Frankfurt 1965 MFH Energy Retrofit

Project: Energy retrofit analysis — 1965 Mehrfamilienhaus (MFH), Frankfurt
Reference typology: TABULA DE.N.MFH.05.Gen.ReEx.001.001
Heated area: 768 m²
Structure: results are logged against the five methodology stages (see `methodology.md`).
Convention: U-values include EN surface films unless stated. THERM Ψ-values use internal dimensions and EN films. Energy balance (interior L2D ≈ exterior L2D) is checked for every THERM model, and the THERM-reported mesh error is recorded as an additional numerical-quality indicator.
Values shown in intermediate equations are rounded for readability; reported Ψ-values are based on the unrounded calculation values.

---

## Stage 1 — Climate Analysis
Status: Complete
Tool: Climate Consultant · Weather: Frankfurt IWEC EPW
Outputs captured (`05_Screenshots`): sun path, psychrometric chart, wind rose, HDD/CDD.
No numeric validation gate — the analysis outputs inform the design rationale (orientation, glazing, summer strategy).

---

## Stage 2 — Summer Radiation / Overheating
Status: Pending
Planned: solar-exposure and overheating-risk assessment of the existing envelope, from the Stage 1 climate data.

---

## Stage 3 — Thermal Bridges (THERM 7.8, EN ISO 10211)

### J1 — Roof–Wall Edge
Date: 2026-07-08

Files:
- `02_Models/01_Before_BASELINE/THERM/20260709_THERM_J1_RoofWallEdge.thm`
- `02_Models/01_Before_BASELINE/THERM/20260708_J1_RoofWallEdge.dxf`
- Materials: `FFM1965_materials.lib`

Cross-section (inverted-L, 1000 mm per leg):
- Wall (interior→exterior): plaster 15 / brick 365 / plaster 15 = 395
- Roof (interior→exterior): plaster 15 / concrete 180 / mineral wool 60 / screed 50
- Corner: concrete slab continues to the outer face of the brick (typical 1965 detail — this concrete path to the façade is why the junction performs poorly)

Materials (λ, W/m·K): Plaster 0.72 · Brick 0.60 · Screed 1.40 · Mineral Wool 0.035 · Concrete 2.00

Boundary conditions:
- Exterior → `EN Exterior -5` (Hc = 25, Rse = 0.04)
- Interior → `EN Interior 20 Wall` (Hc = 7.69; Rsi = 0.13 wall / 0.10 roof)
- Cut ends → Adiabatic

Result:
- L2D = 2.345 W/m·K
- Energy balance: exterior (2.3447) ≈ interior (2.3446), Δ = 0.0001 ✓
- Cross-check: U_wall (THERM) 1.22 = DesignBuilder 1.22 ✓ · U_roof 0.50 ≈ 0.492 ✓
- Mesh error: 0.99% · isotherms dense at corner, parallel at cut ends ✓

```
Ψ = L2D − (U_wall × l_wall) − (U_roof × l_roof)
Ψ = 2.345 − (1.22 × 1.0) − (0.50 × 1.0) = 2.345 − 1.220 − 0.500
```

**⭐ Ψ(J1) = 0.624 W/m·K** (internal dimensions; EN films)

Assessment: J1 has the highest calculated Ψ-value among the five analysed junctions, indicating that the existing roof–wall connection is a significant linear heat-loss path in the current building envelope.

Screenshots (`05_Screenshots/01_Before_BASELINE/THERM`):
- `THERM_J1_Isotherms.png`
- `THERM_J1_Result_Ufactor.png`
- `THERM_J1_Result_Rvalue.png`

### J2 — Window Jamb (Laibung)
Date: 2026-07-10

Objective: installation linear thermal transmittance (Ψ_install) for the original 1965 timber window frame set in the brick reveal.

Files:
- `02_Models/01_Before_BASELINE/THERM/20260710_THERM_J2_WindowJamb.thm`
- `02_Models/01_Before_BASELINE/THERM/20260710_J2_WindowJamb.dxf`
- Materials: `FFM1965_materials.lib` (+ Wood 0.13, Glass 1.00)

Cross-section (horizontal jamb section):
- Wall: plaster 15 / brick 365 / plaster 15 = 395 (extended 1000 mm for 1-D flow at the cut)
- Timber frame (Blendrahmen): 120 × 68, flush with the rebate
- Outer masonry rebate (Anschlag): 50 × 40, flush with the façade (defensible simplification)
- Glazing: 3 / 13 / 3 IGU, U = 2.837
- Installation joint: assumed mortar-filled; modelled as direct frame–masonry contact (negligible effect on Ψ)

Materials (λ, W/m·K): Brick 0.60 · Plaster 0.72 · Wood 0.13 · Glass 1.00 · IGU cavity = Frame Cavity – CEN Simplified (EN ISO 10077-2)

Boundary conditions:
- Wall top + Anschlag → `EN Exterior -5` (Hc = 25, Rse = 0.04)
- Wall bottom + glazing left edge → `EN Interior 20 Wall` (Hc = 7.69, Rsi = 0.13)
- Brick cut end (1 m) → Adiabatic
- Horizontal glazing faces (glass ↔ cavity) → no BC (interior material interface)

Result (Total Length):

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 1.0776 | 1400.5 | 1.509 |
| Exterior | 1.3302 | 1134.5 | 1.509 |

- Energy balance: interior = exterior = 1.509 ✓
- Mesh error: 6.70%. Interior and exterior L2D values are equal to the reported precision; the mesh error is retained transparently as a numerical-quality indicator.

```
Ψ_install = L2D − (U_wall × l_wall) − (U_window × l_window)
Ψ_install = 1.509 − (1.22 × 1.0) − (2.837 × 0.019) = 1.509 − 1.220 − 0.054
```

**⭐ Ψ(J2) = 0.235 W/m·K** (internal dimensions; EN films)

Assessment: Ψ(J2) = 0.235 W/m·K. The calculated value is lower than J1 (0.624 W/m·K), showing a smaller linear heat-loss contribution at the existing window-jamb junction under the modelled conditions.
Methodological note: The first calculation (Ψ ≈ 0.83) was inflated by spurious BCs on the horizontal glazing faces; after removing them and recomputing, the correct value (0.235) was obtained.
Screenshots (`05_Screenshots/01_Before_BASELINE/THERM`):
- `THERM_J2_Isotherms.png`
- `THERM_J2_Isotherms_Zoom.png`
- `THERM_J2_Result_Ufactor.png`
- `THERM_J2_Result_Rvalue.png`

### J3 — Ground Floor–Wall Edge
Date: 2026-07-11

Objective: linear thermal transmittance (Ψ) for the original 1965 ground-floor slab-to-wall junction (slab-on-ground), per EN ISO 10211 / EN ISO 13370.

Files:
- `02_Models/01_Before_BASELINE/THERM/20260711_THERM_J3_GroundFloorWall.thm`
- `02_Models/01_Before_BASELINE/THERM/20260711_THERM_J3b_FloorOnly.thm`
- `02_Models/01_Before_BASELINE/THERM/20260711_J3_GroundFloorWall.dxf`
- Materials: `FFM1965_materials.lib` (+ FloorConcrete 2.30, Soil 2.00)

Cross-section (vertical section; both legs extended 1000 mm for 1-D flow at the cut):
- Wall (interior→exterior): plaster 15 / brick 365 / plaster 15 = 395, seated on the concrete slab
- Ground floor (top→bottom): screed 40 / insulation 10 / concrete slab 180
- Structural sequence: continuous concrete slab first, wall on the slab; the screed + insulation start only at the interior face of the wall (not under it)
- Soil block: 3000 × 3000 mm (≥ 2.5 m each way, per EN ISO 13370)

Materials (λ, W/m·K): Brick 0.60 · Plaster 0.72 · Screed 1.40 · Mineral Wool 0.035 · FloorConcrete 2.30 · Soil 2.00

Boundary conditions:
- Exterior wall face + exterior soil surface → `EN Exterior -5` (Hc = 25, Rse = 0.04)
- Interior wall face + floor top (screed) → `EN Interior 20 Wall` (Hc = 7.69, Rsi = 0.13)
- Wall top, floor cut end, soil base + both soil sides → Adiabatic

Because the floor couples to the ground (not to air), Ψ cannot subtract the raw DesignBuilder U_floor directly (different reference bases). A second flat-floor-on-soil model provides the 1-D floor conductance on the same (with-soil) basis.

Result — corner model (Total Length):

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 0.7495 | 3318.27 | 2.487 |
| Exterior | 1.4239 | 1746.73 | 2.487 |

Energy balance: interior = exterior = 2.487 ✓ · Mesh error 2.94%

Result — flat-floor reference model:

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 0.4819 | 2483.27 | 1.197 |
| Exterior | 2.3160 | 516.728 | 1.197 |

Energy balance: interior = exterior = 1.197 ✓ · Mesh error 6.21%

```
Ψ = L2D_corner − L2D_flat-floor − (U_wall × l_wall)
Ψ = 2.487 − 1.197 − (1.22 × 0.770) = 2.487 − 1.197 − 0.939
```
(l_wall = 0.770 m: the 230 mm slab covers the lower part of the 1000 mm wall)

**⭐ Ψ(J3) = 0.351 W/m·K** (internal dimensions; EN films)

Assessment: Ψ(J3) = 0.351 W/m·K. The calculated value is lower than J1 (0.624 W/m·K) and higher than J2 (0.235 W/m·K) under the modelled conditions. The flat-floor reference model was used to isolate the additional heat flow associated with the ground-floor wall junction.
Screenshots (`05_Screenshots/01_Before_BASELINE/THERM`):
- `20260711_THERM_J3_Result_Ufactor.png`
- `20260711_THERM_J3_Result_Rvalue.png`
- `20260711_THERM_J3b_FloorOnly_Ufactor.png`
- `20260711_THERM_J3b_FloorOnly_Rvalue.png`

### J4 — Entrance Door Threshold (Türschwelle)
Date: 2026-07-11

Objective: linear thermal transmittance (Ψ) for the original 1965 entrance-door threshold at the ground-floor slab (slab-on-ground), per EN ISO 10211 / EN ISO 13370. Two sill constructions were modelled: a masonry (brick) sill — representative of typical 1965 practice and adopted as the project value — and a solid-timber sill as a comparative variant.

Files:
- `02_Models/01_Before_BASELINE/THERM/20260711_THERM_J4_DoorThreshold.thm`
- `02_Models/01_Before_BASELINE/THERM/20260711_THERM_J4_DoorThreshold_WoodSill.thm`
- `02_Models/01_Before_BASELINE/THERM/20260711_J4_DoorThreshold.dxf`
- Flat-floor reference: `02_Models/01_Before_BASELINE/THERM/20260711_THERM_J3b_FloorOnly.thm`
- Materials: `FFM1965_materials.lib`

Cross-section (vertical section through the threshold; door leaf extended 1000 mm for 1-D flow at the cut):
- Door leaf (Türblatt): solid timber, 40 mm, no insulated core — typical 1965 entrance door
- Sill (Schwelle): 68 × 30 mm under the door leaf, seated on the floor build-up
  - Project variant: brick sill (λ = 0.60)
  - Comparative variant: solid timber sill (λ = 0.13)
- Interior floor (right): screed 40 / insulation 10, starting at the interior face of the sill
- Structural slab: concrete 180, continuous under sill and floor
- Soil block: 3000 × 3000 mm (≥ 2.5 m each way, per EN ISO 13370)
- Exterior (left): bare slab / soil surface, no interior build-up
- Installation joints: mortar-filled, modelled as direct contact (negligible effect on Ψ)

Materials (λ, W/m·K): Wood 0.13 · Brick 0.60 · Screed 1.40 · Mineral Wool 0.035 · FloorConcrete 2.30 · Soil 2.00

Boundary conditions:
- Exterior door-leaf face + exterior sill face + bare slab top + exterior soil surface → `EN Exterior -5` (Hc = 25, Rse = 0.04)
- Interior door-leaf face + interior sill face + screed top → `EN Interior 20 Wall` (Hc = 7.69, Rsi = 0.13)
- Door-leaf cut end (top), floor cut end, soil base + both soil sides → Adiabatic

As with J3, the junction couples to the ground; Ψ subtracts the flat-floor-on-soil L2D (same with-soil basis) rather than the raw floor U-value. The 1-D door contribution uses the modelled leaf: U_door = 1 / (0.13 + 0.040/0.13 + 0.04) = 2.09 W/m²·K.

Result — brick sill (project value), Total Length:

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 1.6245 | 2055.47 | 3.339 |
| Exterior | 1.2171 | 2743.48 | 3.339 |

Energy balance: interior = exterior = 3.339 ✓ · Mesh error 5.28%

Result — timber sill (comparison), Total Length:

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 1.5020 | 2055.47 | 3.087 |
| Exterior | 1.1253 | 2743.48 | 3.087 |

Energy balance: interior = exterior = 3.087 ✓ · Mesh error 5.48%

```
Brick sill:  Ψ = 3.339 − 1.197 − (2.09 × 1.0) = +0.049
Timber sill: Ψ = 3.087 − 1.197 − (2.09 × 1.0) = −0.203
```
(flat-floor reference L2D = 1.197, from J3b)

**⭐ Ψ(J4) = 0.049 W/m·K** (brick sill; internal dimensions; EN films) — adopted project value

Assessment: Ψ(J4) = 0.049 W/m·K for the brick-sill variant adopted as the project value. The comparative timber-sill model gives Ψ = −0.203 W/m·K. The approximately 0.25 W/m·K difference between the two variants shows the sensitivity of the junction result to sill material. Under the modelled conditions, the brick-sill threshold has the lowest positive Ψ-value among the five analysed junctions.

Screenshots (`05_Screenshots/01_Before_BASELINE/THERM`):
- `20260711_THERM_J4_Result_Ufactor.png`
- `20260711_THERM_J4_Result_Rvalue.png`
- `20260711_THERM_J4_WoodSill_Result_Ufactor.png`
- `20260711_THERM_J4_WoodSill_Result_Rvalue.png`

### J5 — Balcony Cantilever (auskragende Stahlbetonplatte)
Date: 2026-07-12

Objective: linear thermal transmittance (Ψ) for the original 1965 cantilevered reinforced-concrete balcony slab passing uninterrupted through the masonry wall with no thermal break, per EN ISO 10211.

Files:
- `02_Models/01_Before_BASELINE/THERM/20260712_THERM_J5_BalconyCantilever.thm`
- `02_Models/01_Before_BASELINE/THERM/20260712_THERM_J5b_NoBalcony.thm`
- `02_Models/01_Before_BASELINE/THERM/20260712_J5_BalconyCantilever.dxf`
- Materials: `FFM1965_materials.lib`

Cross-section (vertical section; each wall leg extended 1000 mm for 1-D flow at the cut):
- Wall (interior→exterior): plaster 15 / brick 365 / plaster 15 = 395, above and below the slab
- Intermediate concrete slab: 180 mm, continuous — passes through the full wall thickness and cantilevers 1500 mm to the exterior (no insulation in its path); slab is the balcony structure and the interior floor structure in one piece
- Interior build-up: screed 50 on the slab, gypsum plaster 15 under the slab (ceiling of the room below) — matches "Existing Internal Floor 1965", U = 1.894
- Balcony (exterior): thin sloped screed ~30 on top; slab soffit and cantilever end left bare (typical 1965)
- Modelled at mid-storey level; the balcony is exposed to outside air on three faces (top, soffit, and end)

Materials (λ, W/m·K): Brick 0.60 · Plaster 0.72 · Screed 1.40 · Concrete 2.00 (intermediate slab, per J1)

Boundary conditions:
- Exterior wall faces (above and below) + balcony top + slab soffit + cantilever end → `EN Exterior -5` (Hc = 25, Rse = 0.04)
- Interior wall faces (above and below) + screed top + plaster soffit → `EN Interior 20 Wall` (Hc = 7.69, Rsi = 0.13)
- Wall cut ends (top and bottom) + interior floor cut end → Adiabatic

Result — with-balcony model (Total Length):

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Interior | 0.7561 | 3935 | 2.975 |
| Exterior | 0.6777 | 4390.29 | 2.975 |

Energy balance: interior = exterior = 2.975 ✓ · Mesh error 1.74%

Result — reference model, no cantilever (slab terminated at the façade):

| Surface | U-factor (W/m²·K) | Length (mm) | L2D = U×L/1000 |
|---|---|---|---|
| Exterior | 1.2244 | 2180 | 2.669 |
| Interior | 0.6783 | 3935 | 2.669 |

Energy balance: interior = exterior = 2.669 ✓ · Mesh error 0.75%

```
Ψ = L2D_with-balcony − L2D_no-balcony
Ψ = 2.975 − 2.669 = 0.306
```

**⭐ Ψ(J5) = 0.306 W/m·K** (internal dimensions; EN films)

Assessment: Ψ(J5) = 0.306 W/m·K. The result represents the additional linear heat flow caused by the existing cantilevered concrete balcony slab relative to the otherwise-identical reference model with the cantilever removed. Among the five analysed junctions, J5 has the third-highest calculated Ψ-value after J1 and J3.

Methodological note — why the simple subtraction failed here, and the standard method used:
For J1–J3 the plane components meet the junction as separable paths, so Ψ = L2D − Σ(Uᵢ·ℓᵢ) applies directly. At the balcony, three plane elements (wall above, wall below, and the interior slab) share a common root where the slab crosses the wall; the same material area is claimed by more than one Uᵢ·ℓᵢ term. Subtracting all three (even with correct internal lengths — wall above 950, wall below 985, slab 1000) over-counts this shared area and returns a spurious large negative (≈ −1.28). This is the dimension-convention over-counting artefact described in EN ISO 10211 (a bookkeeping effect, not free energy), and it is the standard signal that the difference method is required for penetrating-element junctions. Ψ was therefore obtained as the difference between the full model and an otherwise-identical reference model with the cantilever removed at the façade; the two models share the same wall and interior slab, so their difference isolates exactly the extra loss caused by the cantilever. The result (+0.306) is positive, physically meaningful, and convention-consistent.

Screenshots (`05_Screenshots/01_Before_BASELINE/THERM`):
- `20260712_THERM_J5_Result_Ufactor.png`
- `20260712_THERM_J5_Result_Rvalue.png`
- `20260712_THERM_J5_Isotherms.png`
- `20260712_THERM_J5b_NoBalcony_Ufactor.png`
- `20260712_THERM_J5b_NoBalcony_Rvalue.png`

### Thermal Bridge Summary

| Junction | Ψ (W/m·K) | Status |
|---|---|---|
| J1 — Roof–Wall Edge | 0.624 | Complete |
| J2 — Window Jamb (Laibung) | 0.235 | Complete |
| J3 — Ground Floor–Wall Edge | 0.351 | Complete |
| J4 — Entrance Door Threshold | 0.049 | Complete |
| J5 — Balcony Cantilever | 0.306 | Complete |

Integration status: The calculated Ψ-values were incorporated into the Run03 DesignBuilder baseline where corresponding linear thermal-bridge input fields were available. J4 (door threshold, Ψ = 0.049 W/m·K) was documented but not applied because no dedicated input field was available.
---

## Stage 4 — Moisture / Condensation

**Status: Pending**

Planned work includes:

- Glaser-method assessment of the existing envelope assemblies
- Review of interior surface temperatures at critical thermal-bridge junctions
- Assessment of condensation and mould-risk locations
- Particular review of the balcony cantilever junction (J5) during the moisture analysis

---

## Stage 5 — Baseline vs. Retrofit (DesignBuilder / EnergyPlus)

### Existing-Building Baseline

**Status: Current benchmarked baseline**

Model: `Frankfurt 1965 BASELINE.dsb`  
Weather: Frankfurt Main Airport, IWEC

Three simulation runs were used to establish and refine the existing-building baseline. Run01 identified a heating-schedule inconsistency. Run02 corrected the heating schedule and established an intermediate baseline using the default DesignBuilder thermal-bridge settings. Run03 retained the corrected heating schedule and incorporated the calculated project-specific thermal-bridge values where corresponding DesignBuilder inputs were available. Run03 is therefore retained as the current benchmarked existing-building baseline.

**Run01 — 2026-07-04 · First attempt (FAILED)**
- Zone Sensible Heating: 58,939 kWh → 76.7 kWh/m²·a (÷ 768 m²)
- Result: Not accepted as the baseline — 76.7 kWh/m²·a, approximately 47.4% below the TABULA original-state reference heating need of 145.9 kWh/m²·a.
- Cause: the NCM heating schedule (`Dwell_DomLounge_Heat`) heats only occupied hours (~17 °C mean, low demand), which is inconsistent with the TABULA/DIN assumption of continuous whole-space heating at setpoint
- Evidence: `05_Screenshots/01_Before_BASELINE/DesignBuilder/20260704_BASELINE_Run01_AnnualHeatBalance.png`

**Fix**
- Heating > Operation > Schedule: `Dwell_DomLounge_Heat` → `On 24/7`
- Single-variable change; all other inputs held constant. This was the sole variable distinguishing Run01 from Run02.

**Run02 — 2026-07-05 · Corrected heating schedule**
- Zone Sensible Heating: 94,302 kWh → 122.8 kWh/m²·a (÷ 768 m²)
- Comparison with TABULA: approximately 15.8% below the TABULA original-state reference heating need of 145.9 kWh/m²·a.
- Status: intermediate baseline run with corrected continuous-heating schedule; default DesignBuilder thermal bridging still active.
- Evidence: `05_Screenshots/01_Before_BASELINE/DesignBuilder/20260705_BASELINE_Run02_AnnualHeatBalance.png`
- Reference: TABULA `DE.N.MFH.05.Gen.ReEx.001.001`, Energy need for heating QH,nd = 145.9 kWh/m²·a.

Key learning: The heating-schedule convention strongly affects benchmark alignment — the NCM intermittent-heating schedule produced substantially lower heating demand than the continuous-heating assumption used for the TABULA comparison.

**Run03 — 2026-07-13 · Baseline with calculated thermal bridges**
- Change from Run02: the calculated THERM Ψ-values were applied where corresponding DesignBuilder linear thermal-bridge input fields were available:
  - Roof–Wall: 0.624 W/m·K (J1)
  - Wall–Ground / External Floor: 0.351 W/m·K (J3)
  - Wall–Floor Internal: 0.306 W/m·K (J5)
  - Window Jamb: 0.235 W/m·K (J2)
- J4 — Entrance Door Threshold (Ψ = 0.049 W/m·K) was documented but not applied because no dedicated DesignBuilder input field was available.
- Corner, Wall–Floor External, Lintel and Sill values remained at their default settings because they were not separately calculated.
- Zone Sensible Heating: 103,138.8 kWh → 134.3 kWh/m²·a (÷ 768 m²)
- Comparison with TABULA: approximately 8.0% below the TABULA original-state reference heating need of 145.9 kWh/m²·a.
- Thermal-bridge impact relative to Run02: +8,836.66 kWh/a → approximately +11.5 kWh/m²·a → +9.4%.
- Status: current existing-building baseline including project-specific calculated thermal bridges.
- Reference: TABULA `DE.N.MFH.05.Gen.ReEx.001.001`, Energy need for heating QH,nd = 145.9 kWh/m²·a.
- Evidence: `05_Screenshots/01_Before_BASELINE/DesignBuilder/20260713_BASELINE_Run03_AnnualHeatBalance.png`

### Run Summary

| Run | Configuration | Annual Heating (kWh) | Heating Demand (kWh/m²·a) | Status |
|---|---|---:|---:|---|
| Run01 | Intermittent NCM heating schedule | 58,939.08 | 76.7 | Failed — schedule inconsistency |
| Run02 | Continuous heating, default thermal bridges | 94,302.14 | 122.8 | Corrected intermediate baseline |
| Run03 | Continuous heating with calculated Ψ-values | 103,138.80 | 134.3 | Current existing-building baseline |

### Retrofit

**Status: Pending**

The retrofit model will be developed from the current Run03 existing-building baseline.

Planned retrofit measures currently include:

- External wall insulation: WDVS / EPS, 160 mm — target U-value ≈ 0.191 W/m²·K
- Roof insulation: mineral wool, 200 mm — target U-value ≈ 0.168 W/m²·K
- Window replacement: triple-glazed Low-E units — target U-value ≈ 0.80 W/m²·K
- Improved airtightness — preliminary modelling target ≈ 0.1 ac/h
- Mechanical ventilation with heat recovery (MVHR) — preliminary heat-recovery efficiency ≈ 80%

The Run03 model will be copied to create `Frankfurt 1965 RETROFIT.dsb`. Only retrofit-related variables will be modified so that climate data, occupancy assumptions, heating setpoints and schedules remain consistent with the existing-building baseline.

Thermal-bridge junctions will be re-modelled in THERM after the retrofit envelope assemblies and junction geometries are defined. Updated retrofit Ψ-values will then be applied to the retrofit DesignBuilder model where corresponding input fields are available.

The final retrofit configuration and performance results will only be reported after the revised model has been simulated and checked.
