# XENTRY Navigation Reference — Offline Clone Laptop, 2016 S550 (W222)

Prepared 2026-08-29 for owner self-diagnosis of a non-working AC. All claims cite a source; anything I could not confirm from a source is marked **UNVERIFIED**.

---

## 1. Which program to open (clone laptops bundle several)

| Program | What it is | Use it for this job? |
|---|---|---|
| **XENTRY Diagnosis / XENTRY OpenShell (XDOS)** | The dealer-level diagnostic UI: quick test, fault codes, live data, actuations, guided tests | **YES — this is the only one you need.** |
| **DAS (Diagnosis Assistance System)** | The older diagnostic front-end for pre-~2010 cars; launched from inside XENTRY for old chassis | No — the 222 chassis is diagnosed in XENTRY proper, not DAS |
| **Vediamo** | Engineering tool (direct ECU coding/flashing), no safeguards, engineer-oriented | **No — do not touch for AC diagnosis** |
| **DTS Monaco** | Vediamo's modern engineering successor (project-file-based ECU interaction) | **No** |
| **WIS / EPC** | Workshop Information System (repair procedures/wiring) and Electronic Parts Catalog | Optional lookup companions |

Sources: benzworld comparison thread (https://www.benzworld.org/threads/xentry-vs-dts-monaco-vs-vediamo-sd-using-sd-connect-c4.3098889/), techroute66 comparison (https://techroute66.com/xentry-vs-vediamo), carsoftz (https://carsoftz.com/blog/dts-monaco-vs-vediamo). Consensus: "XENTRY first; Vediamo/DTS only when deeper engineering access is needed" — and Vediamo "lacks safeguards and requires a high level of expertise." For reading AC codes and running component tests you never leave XENTRY.

OpenShell (XDOS) is the variant built for SDConnect C4/C5/C6 multiplexers; "XENTRY PassThru" is a separate variant that talks to generic J2534 devices instead of the SDConnect toolkit (https://carsoftz.com/blog/xentry-passthru-vs-openshell). Open whichever one matches your interface box.

## 2. Starting a diagnostic session

Step flow (from https://www.obd2tool.com/blog/how-to-use-xentry-diagnosis-for-mercedes/ and https://techroute66.com/mercedes-xentry):

1. **Connect the multiplexer** (SDConnect C4/C5: OBD cable to the port under the driver's-side dash; the C4 can also connect to the laptop via LAN cable or WLAN). Ignition ON, engine off for the initial scan.
2. **Put a battery charger/maintainer on the car before you start.** A long session with ignition on drains the battery, and low voltage causes ECUs to drop off the bus and log garbage undervoltage codes. The obd2tool guide explicitly says to disable battery-intensive accessories to prevent power drain during diagnosis. Exact XENTRY low-voltage warning threshold: **UNVERIFIED** (commonly cited as ~12.0–12.5 V minimum on forums; a maintainer sidesteps the question).
3. **Launch "XENTRY Diagnosis"** (or the "Xentry Cars" icon on some clone images).
4. **Vehicle selection — two ways** (both from the Mercedes icon / vehicle selection tab):
   - **By VIN:** type or auto-read the VIN — preferred, because XENTRY then knows the exact equipment codes (your data card) and shows only the control units your car actually has.
   - **Manual:** Passenger Cars → **222** (S-Class) → your engine/body variant. Use this only if VIN read fails.
5. Wait for the **padlock icon** indicating the connection is established, then press **Start Quick Test**.

## 3. Quick Test — reading, interpreting, clearing

- The Quick Test polls **every control unit** on the car (a W222 has dozens) in roughly a minute and lists them with status flags (https://techroute66.com/mercedes-xentry, https://globaldiags.com/blogs/news/mercedes-xentry-diagnostic-tool-guide):
  - **Green tick** — module responded, no faults
  - **F** — stored (historic) fault(s)
  - **CF** — current AND stored faults (the "C" faults are live right now — chase these first)
- **Reading a code:** double-click the control unit row → **Fault memory** tab → click each fault code to expand the fault text, status (current/stored), and possible causes. Freeze-frame data is under the fault's **environmental conditions / environmental data** view (values captured at the moment the fault set — temp, voltage, speed). Menu label wording varies slightly by XENTRY version: **UNVERIFIED exact label on your build**, but it is always attached to the individual fault entry.
- **Clearing:** each control unit's fault memory view has a **delete/erase fault memory** button; the quick-test screen also offers "delete all fault memories." The obd2tool guide's warning is worth repeating: clearing codes does not fix anything — clear only *after* recording everything (screenshot or photo every fault before you erase), then re-run the quick test after a drive to see what returns as **current**.
- Beginner walk-through thread (benzworld, paywalled to bots but readable in a browser): https://www.benzworld.org/threads/beginners-guide-to-code-reading-xentry-das-star.1959330/

## 4. Getting to the climate control (KLA) unit

1. Run the Quick Test. Find the climate entry in the control-unit list — on Mercedes it is the **KLA (Klima) / "Air conditioning" / "Automatic air conditioning (AAC)"** control unit (naming per https://mercedesdiagnostics.com/guides/climate-diagnostic-guide). On a W222 with rear climate there may also be a separate rear AC entry.
2. Double-click it. Inside a control unit, XENTRY organizes everything into the same standard tabs (per the official XENTRY function list, https://b2bconnect.mercedes-benz.com/gb/workshop-solutions/diagnosis/xentry-diagnosis-system — "Quick test, Actuations, Display of actual and specified values, Guided troubleshooting"):
   - **Version** — hardware/software part numbers (confirm you're in the right unit)
   - **Fault codes / Fault memory** — the B-codes
   - **Actual values** — live data: refrigerant pressure, evaporator temp, in-car/outside temp sensors, sunload sensor, commanded vs actual flap/blend-motor positions (see the AC file for target values)
   - **Actuations** — command components directly: engage the compressor, drive individual blend/air-distribution flap motors, run the blower, cycle the auxiliary pump (https://mercedesdiagnostics.com/guides/climate-diagnostic-guide)
   - **Guided tests / fault paths ("Tests")** — pick a fault code or symptom and XENTRY walks you through measurements step by step with pass/fail branches. On genuine dealer systems some test steps pull data online; on an offline setup expect a subset to work. **UNVERIFIED how much guided-test content is present on any given clone image** — the fault-memory + actual-values + actuations trio is the reliable core.
3. Video reference for the Actual Values & Actuation screens: https://www.tiktok.com/@autoexplaindailyl/video/7640504398493322510 (Xentry Tutorial Ep. 3).

## 5. Clone-laptop gotchas (keep it working, keep it offline)

- **Keep it offline — permanently.** Mercedes servers reject/flag old software, and clone images are commonly configured with `hosts`-file entries such as `127.0.0.1 openshell.aftersales.daimler.com` to stop the software phoning home (http://blog.obdii365.com/2022/08/02/login-2022-06-xentry-openshell-offline/). Do not "fix" networking, do not let Windows Update touch it, and consider disabling the Wi-Fi adapter entirely except if the mux needs WLAN (SDConnect WLAN is laptop↔mux, not internet). Note: XENTRY versions **03.2026 and newer have removed offline login entirely** and require internet (https://autogmt.com/threads/xentry-diagnostics-openshell-and-pass-thru-v03-2026.3757/) — one more reason never to update the working image you have.
- **Date/time sensitivity.** The license "StartKey" is validated against the system clock. If the laptop's date is wrong (dead CMOS battery, timezone sync, manual change), XENTRY throws **"StartKey already expired"** or **"Supplied StartKey is invalid"** at launch/ConfigAssist (https://www.obd2tool.com/blog/xentry-c3-software-activation-startkey-expired-solution/, https://mhhauto.com/Thread-XENTRY-expired-new-key-give-Provided-StartKeyt-is-invalid-in-ConfigAssist). What to know for tomorrow: check the clock shows the real current date **before** launching, and don't change the system date mid-session. If you see those errors, that's a licensing/clock problem, not a car problem — stop there rather than fiddling (fixing licenses is out of scope here).
- **Multiplexer choice.** SDConnect **C4/C5** clones are the standard OpenShell path and fully handle a 2016 W222 (CAN-based diagnosis). C5 is essentially a repackaged C4 (https://www.obd2tool.com/blog/how-to-choose-mb-star-c3-sdconnect-c4-sdconnect-c5-and-vci-clone-c6/). VXDIAG/OpenPort-style J2534 boxes need the **PassThru** flavor of XENTRY instead (https://carsoftz.com/blog/xentry-passthru-vs-openshell). **DoIP (diagnosis over Ethernet) is only mandatory from the 206/223 chassis onward** (per the official PassThru docs, https://b2bconnect.mercedes-benz.com/cy/help/faq/software/xentry-pass-thru-eu) — your 2016 W222 does not need a DoIP adapter for AC work.
- **Voltage again:** keep a charger/maintainer on for the whole session; ECU undervoltage will pollute your quick test with spurious U-codes in many modules and can abort actuations mid-run. (Standard practice; threshold numbers **UNVERIFIED**.)
- **Don't flash/SCN-code offline.** SCN coding and flashing want the online back-end; on an offline clone that path fails or half-completes. AC diagnosis never requires it.

## 6. External resources (usage/navigation only)

Forums / guides:
- https://www.benzworld.org/threads/beginners-guide-to-code-reading-xentry-das-star.1959330/ — the classic beginner code-reading walkthrough for XENTRY/DAS/STAR
- https://techroute66.com/mercedes-xentry — overview of XENTRY functions, quick test, use cases
- https://www.obd2tool.com/blog/how-to-use-xentry-diagnosis-for-mercedes/ — the concrete click-by-click session flow quoted above
- https://globaldiags.com/blogs/news/mercedes-xentry-diagnostic-tool-guide — technician-oriented XENTRY guide (quick-test F/CF legend)
- https://mercedesdiagnostics.com/guides/climate-diagnostic-guide — the best climate-specific XENTRY guide found (KLA live data, actuations, code families)
- https://mhhauto.com/ — MHH Auto forum: the main community for diagnostic-tool usage questions (registration required; ignore the crack-trading threads, the usage/troubleshooting threads are genuinely useful)
- https://mbworld.org/forums/s-class-w222/ — W222-specific owner forum (see the AC file for specific threads)
- https://mbtools.com/guide/vci — plain-English guide to Mercedes VCI/multiplexer hardware options
- Official Mercedes **XENTRY Pass Thru user guide (PDF)**: https://b2bcfrontdoor.azurefd.net/prod/media/tnogt231/en-xpteu-user-guide.pdf — the genuine operation manual; UI navigation matches what clones show
- Official truck-side PassThru manual (same UI concepts): https://service-info.mercedes-benz-trucks.com/media/wysiwyg/DTDPT/Manual_DTDPT_EN.pdf

GitHub (honest assessment: there is **no good "how to drive XENTRY" repo** — GitHub's Mercedes material is reverse-engineering/open-source-replacement work, useful as background):
- https://github.com/rnd-ash/mercedes-hacking-docs — free "Mercedes hacking" book; Chapter 3 covers connecting to the vehicle incl. XENTRY PassThru with a J2534 device and reading its logs. Closest thing to XENTRY documentation on GitHub.
- https://github.com/rnd-ash/OpenVehicleDiag — open-source cross-platform ECU diagnostics app using the PassThru protocol (Mercedes-focused)
- https://github.com/rnd-ash/openStar — open-source diagnostic app for Daimler vehicles "inspired by DAS and Xentry"
- https://github.com/jglim/CaesarSuite — tooling for Daimler CBF diagnostic files (background on how the diagnostics data is structured)
- https://github.com/jakka351/OpenJ2534 — collected J2534/PassThru resources
- Search terms that actually return results: `mercedes-hacking-docs`, `OpenVehicleDiag`, `CaesarSuite`, `xentry` (mostly log parsers), `SDconnect` (mostly firmware chatter). "xentry passthru guide" as a repo does not exist.

## 7. Tomorrow's XENTRY sequence, condensed

1. Charger on car → mux on OBD port → ignition ON → launch XENTRY Diagnosis → select by **VIN**.
2. **Start Quick Test** → photograph the full results list.
3. Open **KLA / Air conditioning** → Fault memory → photograph every code + its environmental data. Check the engine (ME) and front SAM modules too if the compressor never engages.
4. KLA → **Actual values**: refrigerant pressure, evaporator temp, in-car temps, flap positions (targets in the AC file).
5. KLA → **Actuations**: command compressor ON, watch pressure respond; drive each flap motor end-to-end and watch actual position track commanded.
6. Clear codes only after recording; re-test; note what returns as current.
