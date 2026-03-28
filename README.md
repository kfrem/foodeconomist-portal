# FoodEconomist — Restaurant Profit Intelligence Portal

> A single-file HTML business operating system for an independent restaurant profit consultancy based in London. Built to market, sell, diagnose, and manage client relationships — all from one deployable file.

## What This Is

A unified web portal with **three access tiers**:

| Tier | Access | Purpose |
|------|--------|---------|
| **Public** | Anyone visiting the URL | Client-facing demo, value proposition, pricing, contact |
| **Protected** | Unlocked with code `fe2025` | Full diagnostic framework, scripts, acquisition strategy, CRM, revenue tracker |
| **Deep Diagnostic** | Within protected tier | 180 clickable line items with forensic drill-down trees |

**Live URL:** `myprofit.thefoodeconomist.co.uk`  
**Owner:** Godfred Frimpong (WorkMaster Group / The Food Economist)  
**Revenue Target:** £5,000 in first 4 weeks via restaurant profit consulting

---

## Tech Stack

| Component | Technology | Cost |
|-----------|-----------|------|
| Frontend | Single HTML file (HTML/CSS/JS) | £0 |
| Charts | Chart.js 4.4.0 (CDN) | £0 |
| Data Storage | Browser localStorage | £0 |
| Hosting | Hostinger (existing plan) | Already paid |
| Repository | GitHub (kfrem) | £0 |
| Backend (future) | Supabase free tier | £0 |

**Total additional cost: £0**

---

## Project Structure

```
foodeconomist-portal/
├── index.html          # The entire portal (single file, ~310KB)
├── README.md           # This file
├── docs/
│   ├── ARCHITECTURE.md # Technical architecture & code map
│   ├── ROADMAP.md      # Remaining work (55%) with priorities
│   ├── DEPLOY.md       # GitHub → Hostinger auto-deploy setup
│   └── HANDOFF.md      # Developer handoff guide
└── .github/
    └── workflows/
        └── deploy.yml  # GitHub Actions deploy (optional)
```

---

## Quick Start for Developers

### 1. Clone and run locally
```bash
git clone https://github.com/kfrem/foodeconomist-portal.git
cd foodeconomist-portal
# Open directly in browser — no build step, no server needed
open index.html
# Or use any local server:
python3 -m http.server 8000
```

### 2. Make changes
Edit `index.html` directly. The file contains:
- Lines 1–1000: CSS (design system)
- Lines 1000–2400: HTML (all sections/tabs)
- Lines 2400–3900: JavaScript (data, functions, init)

### 3. Deploy
Push to GitHub → auto-deploys to Hostinger (see `docs/DEPLOY.md`).

```bash
git add index.html
git commit -m "description of change"
git push origin main
```

---

## Access Tiers Explained

### Public Tabs (no code needed)
- **Demo** — Interactive P&L with 6 venue types, KPIs, chart, benchmarks, live scenario sliders
- **Energy Audit** — Energy cost calculator with equipment drain analysis
- **Suppliers** — Preferred supplier network with savings estimates
- **Contact** — WhatsApp/Telegram contact with privacy commitment
- **Pricing** — Three-stage service model (no specific fees shown — pricing is flexible)

### Protected Tabs (code: `fe2025`)
- **Full Diagnostic** — 10 categories, 180 line items, venue filtering, clickable drill-down
- **Process Map** — Multi-venue owner flowchart (Mr Hassan example)
- **Proof of Loss** — Printable sample document for walk-in pitches
- **48hr Snapshot** — Step-by-step free snapshot delivery process
- **Scripts** — Sales scripts and objection handling
- **Acquisition** — Client acquisition strategy (Facebook, WhatsApp, walk-ins)
- **4-Week Plan** — Weekly targets to reach £5,000
- **Intake Form** — Enhanced client visit recording with 15+ fields
- **Pipeline** — CRM with status filtering, today's follow-ups, CSV export
- **£5K Tracker** — Revenue progress bar, payment logger, KPI counters
- **Templates** — Copy-paste WhatsApp/email messages for every pipeline stage

---

## Diagnostic Drill-Down System

### How it works
Every diagnostic item has `onclick="drillClick(this, N)"` in the HTML. The `drillClick` function:
1. Extracts text from the clicked element (text nodes only, skips spans)
2. Normalises it (lowercase, strip non-alphanumeric except %)
3. Looks up in `deepTrees` object (5 forensic trees with branches/nodes)
4. Falls back to `drillDown` object (40+ bespoke items with 5-panel detail)
5. Falls back to `getDrillDown()` pattern matcher (covers all 180 items)

### Deep Trees (premium forensic depth)
Currently built for 5 lead items:
1. **Labour cost %** — 3 branches, 14 nodes, legal references, aggregation
2. **Food cost %** — 3 branches, 12 nodes, supplier/waste/pricing analysis
3. **Energy tariff** — 3 branches, 11 nodes, contract/equipment/switching
4. **Menu engineering** — 2 branches, 8 nodes, Stars/Dogs matrix, psychology
5. **Cash flow** — 3 branches, 9 nodes, inflow/outflow/seasonal mapping

### Standard Drill-Down (5-panel)
40+ items with bespoke content covering:
- 💡 What This Means
- 🔍 How to Check
- 💸 Typical Loss
- 🔧 The Fix
- ⏱️ Time to Impact

### Pattern Matcher Fallback
Remaining items get intelligent drill-down based on topic keywords (rates, delivery, VAT, insurance, menu, marketing, cash flow, staffing, tech).

---

## Data Persistence

All client data is stored in browser `localStorage`:

| Key | Contents |
|-----|----------|
| `fe_visits` | Array of client visit/intake records (JSON) |
| `fe_payments` | Array of payment records for revenue tracker (JSON) |
| `fe_unlocked` | Boolean — remembers if user has unlocked protected tier |

**Important:** localStorage is device-specific. Data entered on one device does not sync to another. Future Supabase integration will solve this.

---

## Known Limitations

1. **Single-file architecture** — At 310KB, the file is large but loads fast. Any structural refactoring should preserve the single-file deployment model.
2. **No backend** — All data is in localStorage. No cloud sync, no multi-device access.
3. **Deep trees incomplete** — 5 of 10 categories have full forensic trees. Remaining 5 need building.
4. **Intake form not connected to Supabase** — Form saves locally only.
5. **WhatsApp links use placeholder number** — `447700000000` needs replacing with real number.
6. **No PDF export** — Client reports must be manually created from diagnostic findings.

---

## Revenue Model

| Service | Fee Structure | Notes |
|---------|-------------|-------|
| Free 48hr Snapshot | £0 | Lead generation — costs only time |
| Full Forensic Scan | Tailored (based on size) | One-off, 50% deposit |
| Monthly Monitoring | Tailored (recurring) | Cancel anytime |

Pricing is deliberately not shown on the portal to allow flexible fee negotiation based on business size and capacity to pay.

---

## License

Proprietary. © 2026 Godfred Frimpong / WorkMaster Group / The Food Economist. All rights reserved.
