# W222 (2014–2017 S-Class) AC Failure Diagnosis — 2016 S550, M278 V8

Prepared 2026-08-29. Sources cited per claim; **UNVERIFIED** = could not confirm from a source.

---

## 1. Refrigerant: what your car uses

- **2016 US-market S550: R134a.** Refrigerant capacity charts list the W222 range (S350/S500/S550/S63, 2013→) on **R134a, ~660–870 g depending on rear AC**, with PAG 46 oil (https://database26.com/mercedes-benz-refrigerant-capacity-chart/). Mercedes' CO2 (R744) system appeared only on **European facelift** W222 models (e.g. S560 Euro-spec, 2016–2017) (https://www.mercedes-gym.gr/en/air_conditioners/air-conditioning-systems-r744-co2/, https://mbworld.org/forums/s-class-w222/816664-climate-control-problems-s-class-w-222-freon-r744.html); US cars stayed R134a through the W222 run — Mercedes' broad US switch to R1234yf came with later model years. **The underhood AC service sticker is authoritative** — read it before buying gauges or refrigerant. If it says R1234yf or R744, everything pressure-related below still applies conceptually but the numbers/fittings differ.
- With rear air conditioning (common on S550), total charge is at the high end of the range; there are refrigerant lines running to the rear unit — more joints, more places to leak. Exact charge for your VIN: sticker / data card. (Capacity chart: https://database26.com/mercedes-benz-refrigerant-capacity-chart/)

## 2. Failure modes ranked by likelihood (forum-weighted for W222)

1. **Refrigerant leak — condenser first.** RepairPal: leak is the #1 reported cause of S550 AC-not-working (https://repairpal.com/mercedes-benz/s550/ac-not-working). The condenser sits in the airstream and takes stone damage; one W222 thread found 7–8 inches of debris packed between radiator and condenser (https://mbworld.org/forums/s-class-w222/902868-w222-ac-problem.html). Confirm with UV dye or sniffer — "recharge and see" cycles (that thread: 5 recharges, still broken) waste money.
2. **Refrigerant pressure/temperature sensor** (single combined sensor, mounted at/near the condenser — there is **no separate pressure switch** on the W222). Two documented W222 cases:
   - **B10VA 15** — "refrigerant pressure sensor malfunction, short to positive or open circuit"; symptoms were AC gone warm + cooling fan pinned at max + outside temp reading -33 °C (2014 S350, https://mbworld.org/forums/s-class-w222/868656-w222-fan-constantly-running.html). First check the connector for corrosion; replacing the sensor opens the circuit → full evacuation/refill needed (per that thread).
   - **B119184** — refrigerant pressure implausibly low → compressor locked out. A 2014 S550 showed 0.0 bar on live data after repairs; root cause was a **counterfeit/defective aftermarket sensor** — a genuine OEM sensor fixed it (https://mbworld.org/forums/s-class-w222/916830-2014-s550-c-replacement-compressor-issue.html). Lesson: buy OEM for this part, and trust XENTRY's live pressure reading over guesswork.
3. **Compressor control valve / compressor** — the W222 uses a Denso **7SAS17C** externally-controlled variable-displacement compressor; its **control solenoid valve is "an extremely high failure part"** and is replaceable separately from the compressor (https://www.rkxtech.com/products/rkx-ac-compressor-control-solenoid-valve-for-select-mercedes-denso-7sas17c-diode). Classic control-valve symptoms: slow-to-cool on hot days, works after a few km of driving, intermittent/partial cooling (https://www.atmechanical.com.au/post/a-c-compressor-control-valve-failure, https://www.rycompressors.com/ac-compressor-control-valve-function-symptoms-and-replacement/). The W222 compressor itself is more durable than the W221's (https://www.go-parts.com/garage/a-c-compressor-mercedes-benz-s550-mercedes-benz-cl550-mercedes-benz-s450-2007-2015).
4. **Blend door / air-flap actuators.** Documented 2015 S550 case: weak semi-cold air driver side, warmer passenger side + hissing → dealer found **blend door actuators stuck on both sides** + climate head needed a software update; ~$761 repair, no leak (https://mbworld.org/forums/s-class-w222/837419-2015-s550-air-condition-help.html). One-side-hot/one-side-cold on a W222 points here first (https://www.go-parts.com/garage/hvac-control-mercedes-benz-s-class-mercedes-benz-s-class-maybach-2010-2020).
5. **Heater control valve (A2228303496) / coolant side.** The W222 uses an electric heater control valve regulating coolant into the heater core; stuck-open = heat bleeding into the cabin even with AC running, temp-control complaints (https://carinterior.alibaba.com/question/a2228303496-heater-control-valve-guide). The 837419 owner had previously fixed a heating fault via this valve.
6. **Blower regulator / blower motor** — no or erratic airflow with an otherwise healthy refrigerant loop; "dirty or sluggish blower motor, bad fuse or relay" appear in the generic S-Class cause list (https://www.wheelsjoint.com/mercedes-benz-s-class-ac-not-cooling-causes-and-diagnosis/). W222-specific failure-rate evidence: **UNVERIFIED**.
7. **Sunload sensor** — skews auto climate logic (one side over/under-cools in sun). Listed as a monitored KLA input (https://mercedesdiagnostics.com/guides/climate-diagnostic-guide); W222-specific failure prevalence: **UNVERIFIED**.
8. **Rear AC unit** (rear evaporator/expansion valve/lines) — extra leak points and its own flaps; rear-seat-only complaints go here. W222-specific thread evidence: **UNVERIFIED** (inferred from the rear-AC charge difference in the capacity chart).

## 3. XENTRY KLA live data ("Actual values") — what to look at

(Names per https://mercedesdiagnostics.com/guides/climate-diagnostic-guide and general R134a references; exact label wording varies by XENTRY version.)

| Actual value | Healthy looks like | Notes |
|---|---|---|
| **Refrigerant pressure** | Engine OFF, system equalized ≥30 min: static pressure ≈ R134a saturation pressure for the ambient temp — **~70 psi at 70 °F, ~75–80 psi at 75–80 °F (≈4.8–5.5 bar)** (https://royalrefrigerants.com/blogs/news/r134a-pressure-temperature-chart-explained, PT chart: https://www.igasusa.com/files/R134a-PT-Chart.pdf). Static ≈ ambient saturation only proves *some* liquid refrigerant is present — it cannot prove a full charge. Static near 0 bar = empty system or dead sensor (compare a manifold gauge vs XENTRY: if the gauge shows pressure and XENTRY shows 0.0, the sensor is lying — the exact failure in mbworld thread 916830). | The W222 has ONE combined pressure/temp sensor at the condenser. |
| **Refrigerant pressure, AC running** | Roughly **150–250 psi high side / 25–45 psi low side** at moderate ambient on R134a (https://www.electronicshub.org/ac-pressure-chart/) — XENTRY's single sensor reads the high side; expect it to climb well above static within seconds of compressor engagement. Pressure that never rises = compressor not pumping (control valve/compressor) or empty system. | Numbers are ambient-dependent — use a PT chart, not memory. |
| **Compressor control current / duty cycle** | Should be non-zero and vary with cooling demand (externally-controlled variable compressor). 0 mA commanded = KLA is refusing to run it (check codes: low-pressure lockout like B1191xx). Commanded high but no pressure rise = control valve or compressor mechanical. Exact mA range for the 7SAS17C in XENTRY: **UNVERIFIED**. | |
| **Evaporator temperature sensor** | With AC working hard: pulls down toward **~2–8 °C** and regulates there (prevents icing). Reads ~ambient with AC off. Implausible/-open readings set evaporator-sensor codes (https://mercedesdiagnostics.com/guides/climate-diagnostic-guide). | A W222 thread mechanic flagged evap temp sensor + pressure sensor as the two usual suspects for "recharges then quits" (https://mbworld.org/forums/s-class-w222/902868-w222-ac-problem.html). |
| **In-car / outside temp sensors** | Should match reality within a degree or two. The B10VA case showed **-33 °C outside temp** — a screaming-implausible value pointing at the sensor circuit (https://mbworld.org/forums/s-class-w222/868656-w222-fan-constantly-running.html). | Implausible inputs silently wreck auto-climate logic. |
| **Sunload sensor** | Changes when you cover/shine a light on the dash-top sensor. | |
| **Flap/blend motor positions (specified vs actual)** | Actual tracks specified as you sweep temp settings. Actual frozen while specified moves = stuck/failed actuator (the 837419 "stuck both sides" case). | Pair with Actuations: drive each flap end-to-end and listen. |

## 4. Fault-code families in KLA

W222-documented (from the threads above — these are the real form W222 codes take):
- **B10VA 15** — refrigerant pressure sensor short-to-positive/open (mbworld 868656)
- **B119184** — refrigerant pressure too low / implausible → compressor lockout (mbworld 916830)

Generic Mercedes KLA families (from https://mercedesdiagnostics.com/guides/climate-diagnostic-guide — some of these code numbers are older-chassis style; on the W222 expect the longer Bxxxx-xx format, but the *categories* hold):
- Refrigerant fill/pressure: B1241 (fill level too low → leak), pressure sensor implausible
- Evaporator temp sensor open/short: B1217/B1232 family
- Flap/stepper motor faults: B1262 (defroster flap), B1263 (ventilation flap), B10A207 (air distribution actuator **mechanical fault** = physically blocked flap)
- Compressor: B1269/U1154 (compressor communication/internal), B1419 (clutch, older models)
- Heating side: duo-valve/heater-valve control faults (B1050/B1417 family)
- CAN/LIN communication: B1056/B1029 family — if KLA can't talk to a flap motor on LIN, fix the comm fault before condemning the motor

Reading tip: in XENTRY every code carries current-vs-stored status + environmental (freeze-frame) data — a *stored* pressure code with plausible live pressure now means intermittent (connector!), a *current* one means measure now.

## 5. Diagnostic decision tree

```
1. QUICK TEST (photograph results)
   └─ KLA codes? ── yes → read each + freeze frame → branch by code family (§4)
                 └─ no codes but no cold air → continue

2. KLA ACTUAL VALUES, engine off ≥30 min
   └─ static refrigerant pressure vs ambient PT chart (~70 psi @ 70°F for R134a)
        ├─ ≈ 0 bar → EITHER empty system OR dead sensor
        │     └─ manifold gauge on service port to arbitrate:
        │           gauge 0 too → leak hunt (UV dye/sniffer; condenser + rear lines first)
        │           gauge normal → pressure sensor (OEM only) / wiring
        ├─ ≈ ambient saturation → charge plausibly present → step 3
        └─ wildly high/implausible → sensor circuit (check connector corrosion first)

3. ACTUATION: command compressor ON (engine running, AC max cold)
   ├─ pressure rises briskly, vents get cold → refrigerant loop OK → airflow/flap side (step 4)
   ├─ compressor commanded but pressure barely moves → control solenoid valve (Denso 7SAS17C)
   │     or compressor mechanical; check control current in actual values
   └─ KLA refuses to command it (0 mA) → lockout: low-pressure code, implausible sensor,
         or CAN fault from engine ECU — fix the *reason*, the compressor may be fine

4. AIR SIDE
   ├─ sweep temp 16→28°C both zones; watch specified vs actual flap positions
   │     actual frozen → stuck blend/air-flap actuator (837419 pattern)
   ├─ actuate blower through range → dead/erratic → blower regulator/motor
   └─ AC cold but heat bleeding in → heater control valve stuck open (coolant side)

5. CONFIRM: pressures with AC on vs R134a chart (150–250 psi high / 25–45 psi low, ambient-dependent),
   then leak-detect BEFORE paying for any recharge (dye + 1–2 weeks, or electronic sniffer at
   condenser face, service ports, rear AC line unions).
```

## 6. Symptom-based branches

- **Blows warm both sides, airflow strong:** refrigerant loop — static pressure check first; then compressor engagement (steps 2–3). Most common: leak (condenser) or pressure sensor lockout (https://repairpal.com/mercedes-benz/s550/ac-not-working, mbworld threads above).
- **One side cold, one side warm:** blend flap actuator (stuck — 837419) or heater control valve; refrigerant is fine, don't recharge. Check specified-vs-actual flap positions.
- **No/weak airflow:** blower regulator/motor, clogged cabin filter, or air-distribution flap stuck closed (B10A2-07-style mechanical code).
- **Intermittent — works cold then quits, or only after driving a while:** compressor control solenoid valve is the classic signature (https://www.atmechanical.com.au/post/a-c-compressor-control-valve-failure); also intermittent pressure-sensor connector (corrosion, 868656) and slow leaks ("fine for 2–4 weeks after recharge" = leak, 902868).
- **Works then stops + cooling fan roaring at max / crazy temp display:** pressure/temp sensor circuit (B10VA pattern, 868656).
- **Rear seats warm, front cold:** rear AC unit/its flaps/its lines — check for a rear climate unit in the quick test. (W222 thread evidence: UNVERIFIED.)

## 7. Forum threads — same symptoms, with outcomes

- https://mbworld.org/forums/s-class-w222/916830-2014-s550-c-replacement-compressor-issue.html — 2014 S550, B119184, live pressure 0.0 bar after full repair; **counterfeit aftermarket pressure/temp sensor — OEM sensor fixed it**.
- https://mbworld.org/forums/s-class-w222/868656-w222-fan-constantly-running.html — 2014 S350, warm AC + fan pinned + -33 °C display, **B10VA 15 → pressure sensor / corroded connector**; replacement requires evac/refill.
- https://mbworld.org/forums/s-class-w222/837419-2015-s550-air-condition-help.html — 2015 S550, weak driver-side cooling + hiss; **blend door actuators stuck both sides + climate head software update, ~$761, no leak**.
- https://mbworld.org/forums/s-class-w222/902868-w222-ac-problem.html — W222 S550, cold-for-2-4-weeks-after-recharge cycle (x5) + compressor replaced; unresolved in thread, but veteran poster rejected the dealer's $2,400 A-pillar-actuator quote and pointed at **pressure sensor / condenser-face debris + proper gauge diagnosis**.
- https://forums.mbclub.co.uk/threads/w222-s-class-air-conditioning-not-coming-on.276048/ — W222 AC not engaging at all (UK forum; outcome not extracted — **UNVERIFIED**, read on-site).
- https://mbworld.org/forums/s-class-w222/816664-climate-control-problems-s-class-w-222-freon-r744.html — Euro R744 W222 climate problems (relevant only if your sticker surprisingly says R744).
- https://repairpal.com/mercedes-benz/s550/ac-not-working — aggregated S550 cause ranking (leak > electrical/climate-control > compressor).
- https://www.wheelsjoint.com/mercedes-benz-s-class-ac-not-cooling-causes-and-diagnosis/ — S-Class AC cause checklist incl. cabin filter, condenser-coil cleaning, blower, fuses.
- https://www.obd2tool.com/blog/how-to-fix-mercedes-air-conditioning-w222-not-working/ — W222-specific AC troubleshooting writeup.
- https://mercedes-specialist.uk/blog/mercedes-s-class-w222-common-faults — independent specialist's W222 common-faults list (notes the W222 compressor outlasts the W221's).

## 8. Shopping-list note (only if diagnosis points there)

- Pressure/temp sensor: **OEM only** (counterfeit trap, thread 916830).
- Compressor control solenoid: fits Denso 7SAS17C; **get the version with the diode** — diode versions carry a colored sticker/painted circle on the end (https://www.rkxtech.com/products/rkx-ac-compressor-control-solenoid-valve-for-select-mercedes-denso-7sas17c-diode).
- Any circuit opening (sensor, control valve, condenser) = professional evacuation + recharge to the gram-spec on the sticker afterward.
