# Technical Architecture — FoodEconomist Portal

## File Structure (Single File)

```
index.html
├── <head>
│   ├── Meta tags & viewport
│   ├── Google Fonts (Syne, Epilogue, DM Mono)
│   └── Chart.js 4.4.0 CDN
├── <style> (~1000 lines)
│   ├── CSS Variables (design tokens)
│   ├── Layout components (masthead, nav, sections)
│   ├── Card system
│   ├── Form elements
│   ├── Diagnostic styles (diag-card, diag-item, venue dots)
│   ├── Drill-down styles (drill-panel, drill-row)
│   ├── Multi-venue flowchart styles
│   ├── Proof of loss table styles
│   ├── Pricing grid styles
│   └── Responsive breakpoints (700px, 480px)
├── <body>
│   ├── Masthead (logo, access badge, unlock button)
│   ├── Navigation bar (public + protected tabs)
│   ├── Access gate overlay (password modal)
│   ├── Hero section
│   ├── PUBLIC TABS
│   │   ├── Demo (venue selector, KPIs, chart, P&L, sliders)
│   │   ├── Energy Audit (tariff info, equipment drains, calculator)
│   │   ├── Suppliers (filterable grid)
│   │   ├── Contact (WhatsApp, Telegram, GDPR, process steps)
│   │   └── Pricing (3-stage model, value proposition)
│   ├── PROTECTED TABS
│   │   ├── Full Diagnostic (10 categories, 180 items with onclick)
│   │   ├── Process Map (multi-venue flowchart)
│   │   ├── Proof of Loss (sample document with table)
│   │   ├── 48hr Snapshot (5-step process)
│   │   ├── Scripts (scenarios + objection handling)
│   │   ├── Acquisition (4-step strategy)
│   │   ├── 4-Week Plan (weekly cards + targets)
│   │   ├── Intake Form (15+ field client recording)
│   │   ├── Pipeline (KPIs, filters, visit log table, export)
│   │   ├── £5K Tracker (progress bar, payment logger)
│   │   └── Templates (copy-paste messages)
│   └── <script> (~2500 lines)
│       ├── Access Control (unlock, gate, localStorage persist)
│       ├── Tab Navigation
│       ├── Venue Data (6 venue type objects)
│       ├── Supplier Data (11 supplier objects)
│       ├── Demo Builder (KPIs, chart, P&L, benchmarks)
│       ├── Slider System (scenario builder)
│       ├── Energy Tab Builder
│       ├── Supplier Grid Builder
│       ├── Intake Form Handler (submitIntake → localStorage)
│       ├── Pipeline/CRM (renderVisits, filterPipeline, export)
│       ├── Diagnostic Functions (toggleDiag, filterVenue)
│       ├── Standard Drill-Down Data (drillDown object, 40+ items)
│       ├── Drill-Down Pattern Matcher (getDrillDown function)
│       ├── Deep Tree Data (deepTrees object, 5 forensic trees)
│       ├── Drill-Down Click Handler (drillClick function)
│       ├── Deep Tree Renderer (renderDeepTree function)
│       ├── Standard Drill Renderer (renderStdDrill function)
│       ├── Revenue Tracker (logPayment, renderTracker)
│       ├── Copy Text Helper
│       └── INIT (must be LAST — calls buildVenueChips, buildDemo, etc.)
```

## Critical Code Ordering Rule

**The INIT block MUST be the last executable code in the script.**

All `var` declarations, data objects, and function definitions must appear before:
```javascript
// INIT — RUNS AFTER ALL DEFINITIONS
buildVenueChips();
buildDemo(venues[currentVenue]);
buildSuppliers('all');
renderTracker();
```

If any definition is moved after init, the page will break silently.

## Design System

### CSS Variables
```css
--bg: #0a0a08       /* Page background */
--surface: #161614   /* Card background */
--ink: #f0ede4       /* Primary text */
--ink2: #c8c4b8      /* Secondary text */
--ink3: #8a8678      /* Muted text */
--gold: #c9a84c      /* Brand accent */
--red: #e05545       /* Negative/leak */
--green: #4ade80     /* Positive/saving */
--blue: #60a5fa      /* Info/neutral */
```

### Fonts
- **Syne** (800) — Headings, titles, KPI values
- **Epilogue** (300–600) — Body text, descriptions
- **DM Mono** (400–500) — Labels, tags, monospace data

### Component Patterns
- Cards: `.card` with `.card-title` and `.card-sub`
- KPI strips: `.kpi-strip` > `.kpi` > `.kpi-label` + `.kpi-val`
- Forms: `.form-grid` > `.form-group` > `.form-label` + `.form-input`
- Diagnostic: `.diag-card` > `.diag-header` + `.diag-body` > `.diag-items` > `.diag-item`

## Drill-Down Architecture

### Lookup Chain
```
User clicks .diag-item
    → drillClick(el, idx) extracts text nodes
    → normalise(text): lowercase, strip non-alphanumeric (keep %)
    → check deepTrees keys (fuzzy match via normalised comparison)
    → if match: renderDeepTree() — multi-level expandable tree
    → else check drillDown keys (fuzzy match)
    → if match: renderStdDrill() — 5-panel standard detail
    → else: getDrillDown(text) — pattern matcher fallback
    → renderStdDrill() with generated content
```

### Deep Tree Data Structure
```javascript
deepTrees = {
  "Item text": {
    overview: "String — what this diagnostic area covers",
    branches: [
      {
        id: "A",
        title: "Branch name",
        desc: "Branch description",
        nodes: [
          {
            title: "Node name",
            detail: "Node explanation",
            subs: ["Sub-item 1", "Sub-item 2", ...]
          }
        ]
      }
    ],
    aggregation: {
      title: "Output statement name",
      outputs: ["Output line 1", "Output line 2", ...]
    }
  }
}
```

### Standard Drill-Down Data Structure
```javascript
drillDown = {
  "Item text": {
    explain: "What this means in plain English",
    check: "How to check/verify in the restaurant",
    loss: "Typical monetary loss with calculations",
    fix: "Specific actions to fix the issue",
    time: "How long until the fix shows results"
  }
}
```

## localStorage Schema

### fe_visits (Array of Objects)
```json
{
  "restaurant_name": "String",
  "owner_name": "String",
  "phone": "String",
  "email": "String",
  "address": "String",
  "venue_type": "String",
  "covers": "String",
  "weekly_revenue": "String",
  "spoke_to": "String (comma-separated)",
  "reaction": "String",
  "objections": "String (comma-separated)",
  "materials": "String",
  "status": "hot|warm|followup|booked|converted",
  "followup_date": "YYYY-MM-DD",
  "source": "walk-in|whatsapp|facebook|referral|google-maps|other",
  "next_action": "String",
  "notes": "String",
  "docs_collected": "String (comma-separated)",
  "visit_date": "ISO datetime"
}
```

### fe_payments (Array of Objects)
```json
{
  "client": "String",
  "amount": "Number",
  "type": "snapshot|deposit|scan-full|retainer|other",
  "date": "YYYY-MM-DD"
}
```
