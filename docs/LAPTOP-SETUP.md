# XENTRY Laptop Prep — before connecting to the car

## 1. Network posture: "never call home" vs. Claude needs internet

These two goals conflict, so be deliberate about it:

- **Claude Code needs internet** (api.anthropic.com). Fully air-gapping the
  laptop means no Claude on it.
- **XENTRY must not reach Mercedes/Daimler servers.** Clone installs normally
  ship with this already blocked. Verify rather than assume:

### Verify the blocks (PowerShell as admin)
```powershell
# 1. hosts file — clone vendors usually blackhole Daimler domains here
Get-Content C:\Windows\System32\drivers\etc\hosts | Select-String -Pattern "daimler|mercedes|xentry|corpinter"

# 2. Windows Firewall — look for outbound block rules on XENTRY executables
Get-NetFirewallRule | Where-Object {$_.DisplayName -match "xentry|das|mercedes"} | Format-Table DisplayName,Direction,Action

# 3. Disable XENTRY update / telemetry services if present
Get-Service | Where-Object {$_.DisplayName -match "Xentry|DAS|AddOn|Update"} | Format-Table Name,Status,StartType
```

If the hosts file has no blocks, add outbound firewall block rules for the
XENTRY install folder's executables (safer than editing hosts, and it survives
updates). Belt-and-suspenders: do the diagnostic session itself with Wi-Fi off,
and only reconnect when you want to talk to Claude.

**Practical rhythm that satisfies both:** Wi-Fi OFF while XENTRY talks to the
car → screenshot results → Wi-Fi ON to consult Claude Code → Wi-Fi OFF for the
next XENTRY step. Clunky but airtight. If the blocks verify clean, staying
online the whole time is also reasonable — your call.

## 2. Claude Code vs. Claude Desktop on the laptop

**Claude Code (already installed) is the right tool — you don't need Claude
Desktop.** Neither one can drive the XENTRY GUI for you (XENTRY is a native
Windows app; there's no browser to automate). What Claude Code does well:

- **Reads screenshots.** Snip the XENTRY screen (`Win+Shift+S`), save the PNG
  into `sessions/screenshots/`, then in Claude Code: *"read
  sessions/screenshots/quicktest.png and tell me what these codes mean and where
  to go next."* Claude Code reads images natively.
- **Has all the reference docs local** once this repo is cloned — it can answer
  "which actuation tests the compressor control valve" from `docs/` without you
  re-explaining anything.
- **Keeps the session log** in `sessions/` as you dictate findings.

Claude Desktop would only add a chat window; it has no advantage here and is
one more thing phoning out from a laptop you want quiet.

Log in on the laptop with `claude` → it uses the Max subscription (OAuth) — do
not paste an API key.

## 3. Hardware checklist before the session

- [ ] **Battery charger/maintainer on the car.** XENTRY sessions with ignition
      on for 30–60 min will sag the battery; low voltage causes phantom fault
      codes in every module and can abort tests.
- [ ] Multiplexer (SDconnect C4/C5 or VXDIAG) connected and its firmware/
      config already known-good (test connection in XENTRY before starting).
- [ ] Engine will need to RUN for AC pressure/compressor tests — do it outside
      or with ventilation.
- [ ] Phone camera as backup for screens you can't snip (e.g., full-screen
      XENTRY moments).
- [ ] Thermometer for vent-outlet temps (a cheap probe thermometer in the
      center vent — objective before/after data).

## 4. Clone this repo onto the laptop

```powershell
git clone https://github.com/qvidal01/w222-xentry-diag.git
cd w222-xentry-diag
claude
```

(If git isn't on the laptop, download the repo ZIP from GitHub instead.)
