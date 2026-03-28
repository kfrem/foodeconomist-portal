# CLAUDE CODE INSTRUCTIONS — FoodEconomist Portal Deployment

## CONTEXT
This project was built in Claude.ai chat over multiple sessions. The complete working portal is the index.html file in this same folder. All documentation is in the docs/ folder. Everything is ready — it just needs pushing to GitHub and connecting to Hostinger.

## WHAT YOU NEED TO DO

### Step 1: Create GitHub repo and push everything
```bash
cd ~/foodeconomist-portal
git init
git branch -M main
git add .
git commit -m "Initial commit: FoodEconomist Restaurant Profit Intelligence Portal"
gh repo create foodeconomist-portal --private --source=. --push
```

If `gh` is not authenticated, run `gh auth login` first.

### Step 2: Verify
```bash
gh repo view kfrem/foodeconomist-portal --web
```

### Step 3: Tell the user
Once pushed, tell the user to:
1. Go to Hostinger hPanel → their website → Advanced → Git
2. Connect to https://github.com/kfrem/foodeconomist-portal.git
3. Branch: main
4. Directory: /public_html/myprofit
5. This enables auto-deploy on every git push

## PROJECT OVERVIEW

This is a single-file HTML portal (index.html, ~310KB) for a London-based restaurant profit consultancy. It has:

### Public-facing tabs (no login needed):
- **Demo** — Interactive P&L with 6 restaurant venue types, KPIs, Chart.js charts, benchmark bars, live scenario sliders
- **Energy Audit** — Energy cost calculator showing deemed vs fixed rate savings
- **Suppliers** — Filterable preferred supplier grid with savings estimates  
- **Contact** — WhatsApp/Telegram CTAs with GDPR commitment
- **Pricing** — Three-stage service model (fees deliberately hidden — owner charges flexibly)

### Protected tabs (unlock code: fe2025):
- **Full Diagnostic** — 10 categories, 180 clickable line items with drill-down
- **Process Map** — Multi-venue owner flowchart example
- **Proof of Loss** — Printable sample document for walk-in pitches
- **48hr Snapshot** — Step-by-step free snapshot delivery process
- **Scripts** — Sales scripts and objection handling
- **Acquisition** — Client acquisition strategy (Facebook, WhatsApp, walk-ins)
- **4-Week Plan** — Weekly targets to reach £5,000
- **Intake Form** — 15+ field client visit recording (saves to localStorage)
- **Pipeline** — CRM with status filtering, follow-ups, CSV export
- **£5K Tracker** — Revenue progress bar and payment logger
- **Templates** — Copy-paste WhatsApp/email messages

### Diagnostic drill-down system:
- 180 items with inline onclick handlers
- 5 deep forensic trees (Labour, Food Cost, Energy, Menu Engineering, Cash Flow) with multi-level expandable branches
- 40+ bespoke standard drill-down items with 5-panel detail
- Pattern-matching fallback for remaining items

## CRITICAL TECHNICAL RULES

1. **Single file architecture** — Everything is in index.html. Never split it.
2. **var not const/let** — All top-level declarations use `var` to avoid temporal dead zone errors
3. **Init calls MUST be last** — The init block (buildVenueChips, buildDemo, etc.) must be the final executable code in the script
4. **Inline onclick** — Every .diag-item has onclick="drillClick(this,N)" directly in HTML
5. **No specific prices in public sections** — Owner charges flexible fees

## REMAINING WORK (~55%)

See docs/ROADMAP.md for full details. Key priorities:
1. Build 5 more deep forensic trees (Premises, Delivery, Finance, Capacity, Marketing)
2. Upgrade 135 standard drill-down items to bespoke content
3. Connect Supabase for cloud data storage (replace localStorage)
4. Build client-facing data collection questionnaire
5. Auto-generate PDF reports from diagnostic findings
6. Mobile optimisation
7. Replace WhatsApp placeholder number (447700000000) with real number

## FILE STRUCTURE
```
foodeconomist-portal/
├── index.html              # The entire portal (~310KB, ~3900 lines)
├── README.md               # Project overview
├── .gitignore              # Standard ignores
├── CLAUDE_CODE_INSTRUCTIONS.md  # This file
└── docs/
    ├── ARCHITECTURE.md     # Technical code map
    ├── ROADMAP.md          # Remaining work with hour estimates
    ├── DEPLOY.md           # GitHub → Hostinger setup guide
    └── HANDOFF.md          # Developer handoff guide
```

## OWNER INFO
- **Name:** Godfred Frimpong
- **Business:** WorkMaster Group / The Food Economist  
- **GitHub:** kfrem
- **Hosting:** Hostinger (thefoodeconomist.co.uk)
- **Subdomain:** myprofit.thefoodeconomist.co.uk
- **Prefers:** Email-only, no phone/video, behind-the-scenes operation
