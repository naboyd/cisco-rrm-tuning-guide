# Cisco Wireless RRM Tuning Guide

Standalone HTML reference for **Catalyst 9800 classic RRM** and **Catalyst Center 3.x AI-Enhanced RRM**, including deployment profiles, positive/negative impact notes, and a classic-vs-AI control matrix.

## Quick start

1. Open `index.html` in any modern browser (Chrome, Edge, Safari).
2. Use the **View** dropdown at the top to switch sections.

No server, build step, or dependencies required.

```bash
# macOS
open index.html

# Or from this directory
python3 -m http.server 8080
# Then browse to http://localhost:8080
```

## Views in the guide

| View | Purpose |
|------|---------|
| **Deployment Profiles** | Six tailored profiles — default view; C9800 Default vs recommended per setting |
| **Classic vs AI Matrix** | Which settings are WLC-only, AI RF Profile, edge (CHD/ED-RRM), or WLAN |
| **BP Comparison** | C9800 defaults vs Cisco published guidance |
| **9800 Classic RRM** | Full classic RRM feature reference with tradeoffs |
| **Catalyst Center AI RRM** | AI-Enhanced RRM services, busy hour, Insights/Simulator |
| **CLI Reference** | Common `show` and `ap dot11` commands |
| **AI Show-Tech Analysis Prompt** | Copy-paste prompt for analyzing `show tech-support wireless` (profile-aware) |

## How to use deployment profiles

1. Select **Deployment Profiles** in the View dropdown.
2. Pick your environment from **Deployment** (e.g. Multi-Tenant for shared high-rise).
3. Review **Recommended settings** — each row lists rationale plus **positive** and **negative** impacts.
4. Cross-check **Deployment profile comparison** at the bottom of that tab — amber cells and **≠** mark values that differ from C9800 factory defaults.
5. Open **CLI Reference** for copy-paste commands for your profile.

Before changing production RRM: export current config, schedule a maintenance window for RF profile pushes, and validate with `show ap dot11 {band} summary` after changes.

## AI show-tech analysis

1. Open **AI Show-Tech Analysis Prompt** (last item in the View menu).
2. Choose **Analyze as profile** (e.g. Stadium) — the prompt updates with that profile's Cisco targets, rules, and CLI.
3. Click **Copy prompt** and paste into your AI assistant.
4. Append or attach `show tech-support wireless` output below the prompt line.
5. Use **Auto-detect** when the WLC serves multiple site types and you want the AI to map each site to an archetype.
6. Redact PSKs and secrets before using external AI tools.

## Classic vs AI-Enhanced RRM

- **One WLC runs classic or AI — not both.** Check with `show ap dot11 5ghz group` (Auto-Leader = classic; Remote-Member = AI enrolled).
- **AI services** (DCA, TPC, FRA, DBS): configure in Catalyst Center **AI RF Profile** when enrolled.
- **Edge settings** (CHD, ED-RRM, DFS): remain on the WLC in both modes.
- **WLAN settings** (band select, client steering): always on the WLC.

See the **Classic vs AI Matrix** tab for the full ownership table.

## Sources

- Cisco C9800 Configuration Guide (RRM / RF Profile — university HD example)
- WLC RF Management Best Practices
- CX Large Public Networks Design Guide
- C9800 Series Configuration Best Practices (site tags for stadium/campus HD)
- Catalyst Center AI-Enhanced RRM Deployment Guide

## Repository setup (Cisco Git)

This repo is initialized locally. To connect your **Cisco enterprise** remote (not personal GitHub):

```bash
cd /path/to/cisco-rrm-tuning-guide
git remote add origin <YOUR_CISCO_GIT_URL>
git push -u origin main
```

Use your Cisco Git credentials or SSO as required by your org. Commit author email on this machine may differ from `naboyd@cisco.com` — set per your org policy before pushing.

## Files

| File | Description |
|------|-------------|
| `index.html` | Self-contained tuning guide (all CSS/JS inline) |
| `RRM-Settings-Source-References.docx` | Setting-by-setting Cisco document source matrix |
| `scripts/build_source_references_docx.py` | Regenerates the .docx from source data |
| `README.md` | This file |

Regenerate the source document after guide changes:

```bash
cd /path/to/cisco-rrm-tuning-guide
python3 -m venv .venv
.venv/bin/pip install python-docx
.venv/bin/python scripts/build_source_references_docx.py
```

## License

Internal Cisco use — confirm with your team before external distribution.
