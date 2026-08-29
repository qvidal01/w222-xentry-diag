# NotebookLM Gap Analysis — reviewed 2026-08-29

Compared the two personal-account notebooks against outside research:
- **"Xentry"** — 93 sources
- **"Xentry Passthru | Openshell Software | Mercedes-Benz"** — 51 sources (almost entirely YouTube install/setup videos; large overlap with the first notebook)

## What the notebooks already cover well

- **Software ecosystem & install:** XENTRY OpenShell/XDOS install, PassThru vs full
  Diagnosis kits, Xentry Lite, HHTWIN, running without VMware
- **Hardware:** SDConnect C4/C5 firmware, VXDIAG VCX SE, Openport 2.0 / J2534
  comparisons — good coverage for multiplexer troubleshooting
- **Basic usage:** several "how to use XENTRY" tutorials including one specifically
  on **Actual Values** — watch that one before tomorrow if any
- **Companion tools:** StarFinder (wiring diagrams — genuinely useful if the AC fault
  turns electrical), EPC (parts lookup), WIS/ASRA (factory repair procedures)
- **Official context:** B2B Connect, SERMI, subscription/licensing landscape
- **Engineering tools:** DTS Monaco and Vediamo installs — **not needed for AC
  diagnosis; skip all of this tomorrow**

## What was missing (now filled by this repo)

1. **AC/climate diagnosis — the actual job.** Nothing in either notebook mentions the
   KLA control unit, refrigerant pressures, the compressor, fault codes, or any
   W222 AC failure mode. `w222-ac-diagnosis.md` is the missing half.
2. **W222-specific case studies.** The MBWorld threads with real codes and outcomes
   (B10VA 15 pressure sensor, B119184 counterfeit-sensor lockout, stuck blend doors)
   — none were in the notebooks. Added to the "Xentry" notebook 2026-08-29.
3. **A diagnostic sequence.** The notebooks teach the software; nothing sequences
   quick test → static pressure vs PT chart → actuation → air side. That decision
   tree is in `w222-ac-diagnosis.md` §5.

## GitHub verdict (asked and answered)

There is **no useful "navigate XENTRY" repo on GitHub** — that ecosystem is
reverse-engineering work (`rnd-ash/mercedes-hacking-docs` is the only partially
relevant item; its ch. 3 covers XENTRY PassThru connection). Real navigation
documentation lives on forums (BenzWorld, MHH Auto), the walkthrough sites cited in
`xentry-navigation.md`, and Mercedes' official PassThru user-guide PDF. The
notebooks + this repo now cover essentially everything publicly available.

## Practical notes for tomorrow

- The notebooks skew ~70% toward install/coding content that is irrelevant to an AC
  diagnosis. Tomorrow's session touches only: connect → quick test → KLA → actual
  values → actuations. Everything needed is in this repo's two docs.
- If the fault turns electrical (wiring to the pressure sensor or a flap motor),
  **StarFinder** (already installed on most clone laptops, covered in the notebook)
  has the W222 wiring diagrams — that's the moment the notebook content pays off.
