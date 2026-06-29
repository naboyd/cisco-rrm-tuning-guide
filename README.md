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
| **Deployment Profiles** | Tailored settings for Enterprise Campus, Multi-Tenant, NYC Downtown, Atlanta Downtown — with positive/negative impact per change |
| **Classic vs AI Matrix** | Which settings are WLC-only, AI RF Profile, edge (CHD/ED-RRM), or WLAN |
| **BP Comparison** | C9800 defaults vs Cisco published guidance |
| **9800 Classic RRM** | Full classic RRM feature reference with tradeoffs |
| **Catalyst Center AI RRM** | AI-Enhanced RRM services, busy hour, Insights/Simulator |
| **CLI Reference** | Common `show` and `ap dot11` commands |

## How to use deployment profiles

1. Select **Deployment Profiles** in the View dropdown.
2. Pick your environment from **Deployment** (e.g. Multi-Tenant for shared high-rise).
3. Review **Recommended settings** — each row lists rationale plus **positive** and **negative** impacts.
4. Cross-check **Four-way deployment comparison** at the bottom of that tab.
5. Open **CLI Reference** for copy-paste commands for your profile.

Before changing production RRM: export current config, schedule a maintenance window for RF profile pushes, and validate with `show ap dot11 {band} summary` after changes.

## Classic vs AI-Enhanced RRM

- **One WLC runs classic or AI — not both.** Check with `show ap dot11 5ghz group` (Auto-Leader = classic; Remote-Member = AI enrolled).
- **AI services** (DCA, TPC, FRA, DBS): configure in Catalyst Center **AI RF Profile** when enrolled.
- **Edge settings** (CHD, ED-RRM, DFS): remain on the WLC in both modes.
- **WLAN settings** (band select, client steering): always on the WLC.

See the **Classic vs AI Matrix** tab for the full ownership table.

## Sources

- Cisco C9800 Configuration Guide (RRM)
- WLC RF Management Best Practices
- CX Large Public Networks Design Guide
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
| `README.md` | This file |

## License

Internal Cisco use — confirm with your team before external distribution.
