# SSTK Component QC Inspection Log
### Component Quality Control System — Lab Sensor & Sistem Telekontrol, UGM

> ⚠️ **DISCLAIMER: All inspection records in this workbook are simulated / dummy data generated for portfolio demonstration purposes only. This is not real laboratory data from Universitas Gadjah Mada or any other institution.**

---

## Overview

A **formula-driven Excel workbook** implementing a structured incoming component inspection system for the Lab Sensor & Sistem Telekontrol (SSTK), Dept. of Nuclear Engineering & Engineering Physics, Universitas Gadjah Mada.

Covers **4 practicum courses** with ~80 students/week across 4 sessions (Sesi A–D):

| Sheet | Practicum | Components |
|-------|-----------|-----------|
| `Elek_Analog` | Elektronika Analog | Resistor, Capacitor, Diode, Transistor, Op-Amp, Voltage Reg |
| `Elek_Digital` | Elektronika Digital | IC Logic Gates, Relay, Switch, LED, Timer IC |
| `Sistem_Instr` | Sistem Instrumentasi | Temp/Pressure/Motion Sensors, RTD PT100, 4–20mA Transmitter, MCU |
| `Jar_Komunikasi` | Jaringan Komunikasi | RF/BT/LoRa Modules, RS-485, CAN Bus, Relay, Terminal Block |
| `Defect Log` | — | Consolidated defect tracker (root cause, corrective action, status) |
| `Defect Analysis & Trend` | — | Pareto charts per practicum + monthly defect rate trend |
| `Dashboard` | — | Cross-practicum KPI summary (zero manual input) |

---

## Formula Architecture

**Design principle: minimal manual input, maximum automation.**

Only these columns require manual input per inspection record:

| Input (Yellow) | Formula Auto-Calculated (Gray) |
|----------------|-------------------------------|
| Visual inspection (Pass/Fail) | **Test 1 Result** — Pass if measured value within ±10% of spec |
| Spec / rated value | **Overall Result** — PASS only if ALL three tests pass |
| Measured value | **Remarks** — "Release to practicum" or "Quarantine" |
| Functional test name | |
| Test 2 result (Pass/Fail) | |
| Component type | |

```
Test 1 Result  = IF(Visual="Fail", "Fail",
                   IF(ABS(Measured−Spec)/Spec ≤ 10%, "Pass", "Fail"))

Overall Result = IF(AND(Visual="Pass", Test1="Pass", Test2="Pass"),
                   "PASS", "FAIL")

Remarks        = IF(Overall="PASS",
                   "Release to practicum",
                   "Quarantine — do not issue to students")
```

**Dashboard** and **Defect Analysis** pull all values via cross-sheet COUNTIFS formulas — no manual input needed after inspection data is entered.

> **735+ formula cells** across all 7 sheets.

---

## Inspection Workflow

```
Receive component batch
        ↓
Visual inspection → record Pass/Fail            [MANUAL]
        ↓
Measure value (multimeter/LCR meter) → record   [MANUAL]
        ↓
Test 1 Result: auto-calculated (±10% tol.)      [FORMULA]
        ↓
Functional test (logic/switching/comm) → record [MANUAL]
        ↓
Overall Result: auto (all tests must pass)       [FORMULA]
        ↓
Disposition: auto (release / quarantine)         [FORMULA]
        ↓
FAIL records → Defect Log → Root cause → Corrective action
```

**Test equipment:** Multimeter (Sanwa CD771), LCR Meter, Oscilloscope (GDS-1022),
DC Power Supply (HY3005F), Function Generator, Arduino Uno (test harness).

---

## Defect Analysis

### Pareto (per practicum)
Each practicum sheet has a dedicated pareto table with 4 defect categories:

| Category | Description |
|----------|-------------|
| Measured Value OOSpec | Passes visual but fails ±10% tolerance test |
| Visual Defect | Physical damage, bent pins, housing cracks |
| Functional Test Fail | Communication/switching/logic failure |
| Both Tests Fail | Multiple failure modes |

Count, % of total, and cumulative % are all **formula-driven** from the inspection log sheets.

### Monthly Trend
Manual input: Month, Total Inspected, defect counts by category, Target Rate.
Auto-calculated: Total Defects, Defect Rate (%), Status vs Target.
Line chart shows actual defect rate vs 5% target across 12 months.

---

## PDF Export

Workbook is pre-configured for clean A4 PDF export:

| Sheet | Orientation | Layout |
|-------|-------------|--------|
| Dashboard | Portrait | Fit to 1 page |
| Inspection Logs (×4) | Landscape | Fit to width, header row repeats |
| Defect Log | Landscape | Fit to width |
| Defect Analysis & Trend | Landscape | Fit to width |

To export: **File → Export → Create PDF/XPS → Publish**

---

## Context

Developed based on practical experience assisting component QC inspection at Lab SSTK, Dept. of Nuclear Engineering & Engineering Physics, UGM — covering:

- Visual inspection of relay, switch, sensor, and IC components
- Coil resistance measurement and switching response verification (multimeter)
- Continuity testing and functional verification before issuing to practicum students
- Pass/fail logging and component quarantine for defective units

The inspection workflow and component categories are directly applicable to **incoming inspection (IPQC)** roles in electronic component manufacturing — particularly for relay, switch, and sensor products.

---

## Files

| File | Description |
|------|-------------|
| `SSTK_Component_QC_Log.xlsx` | Main workbook — 7 sheets, 735+ formulas, PDF-ready |

---

## Author

**Naufal Suryo Saputro**
Bachelor of Engineering, Engineering Physics — Universitas Gadjah Mada (Jan 2026)
[LinkedIn](https://linkedin.com/in/naufal-suryo) | [GitHub](https://github.com/suryonaufal)

---

*⚠️ Simulated data — for portfolio demonstration only.*
