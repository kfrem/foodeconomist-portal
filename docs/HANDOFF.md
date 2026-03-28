# Developer Handoff Guide

## Context

This project is a business-critical tool for a solo restaurant profit consultant in London. The owner (Godfred Frimpong) does not code — he uses Claude AI to build and modify this portal. If Claude is unavailable, this document enables any web developer to continue the work.

---

## Critical Rules

### 1. SINGLE FILE ARCHITECTURE — DO NOT BREAK
The entire portal is one `index.html` file. This is deliberate:
- Deploys by copying one file
- No build step, no dependencies, no npm
- Works offline for demos
- Owner can upload via Hostinger file manager if git breaks

**Never** split into multiple files unless explicitly requested.

### 2. JAVASCRIPT EXECUTION ORDER
The `<script>` block has a strict ordering requirement:

```
1. var declarations (data objects: venues, suppliers, drillDown, deepTrees, etc.)
2. function definitions (all functions)
3. INIT calls (buildVenueChips, buildDemo, etc.)
```

**INIT must be the LAST thing in the script.** If any function or data object is defined AFTER the init calls, the page will fail silently.

When adding new features, always add code ABOVE the init block.

### 3. USE `var` NOT `const` OR `let` FOR TOP-LEVEL DECLARATIONS
The file has data objects (drillDown, deepTrees, venues) and functions scattered across ~2500 lines of JS. Using `const` or `let` creates "temporal dead zones" that cause silent failures when functions reference objects declared later in the file. `var` hoists properly and avoids this entirely.

### 4. NO SPECIFIC PRICING IN PUBLIC-FACING SECTIONS
The owner charges flexible fees based on client size. Public tabs must NEVER show specific prices (£750, £500, etc.). Protected tabs (admin-only) may reference prices as internal guidance.

### 5. DIAGNOSTIC DRILL-DOWN USES INLINE ONCLICK
Every `.diag-item` has `onclick="drillClick(this, N)"` directly in the HTML. This is the most reliable approach — no event delegation timing issues, no DOMContentLoaded dependencies. When adding new diagnostic items, include the onclick attribute.

### 6. TEXT MATCHING USES NORMALISATION
The drill-down system matches clicked text to data object keys by normalising both: `text.toLowerCase().replace(/[^a-z0-9%]/g, '')`. This handles encoding differences (en-dashes, em-dashes, unicode escapes). When adding new drillDown or deepTrees entries, the key text does not need to be character-perfect — just close enough to normalise to the same string.

---

## Common Tasks

### Add a new diagnostic item
1. Find the relevant category in the HTML (`diag-card` section)
2. Add inside the `diag-items` div:
```html
<div class="diag-item" onclick="drillClick(this,181)" style="cursor:pointer">
  <span class="venue-dot" style="background:var(--gold)"></span>
  Your new item text here
</div>
```
3. Add the drill-down content in the `drillDown` object:
```javascript
"Your new item text here": {
  explain: "...",
  check: "...",
  loss: "...",
  fix: "...",
  time: "..."
},
```

### Add a new deep forensic tree
Add to the `deepTrees` object following this structure:
```javascript
"Item text matching the HTML": {
  overview: "What this diagnostic area covers",
  branches: [
    {
      id: "A",
      title: "Branch name",
      desc: "Branch description",
      nodes: [
        {
          title: "Node name",
          detail: "Detailed explanation",
          subs: ["Sub-point 1", "Sub-point 2"]
        }
      ]
    }
  ],
  aggregation: {
    title: "Output statement name",
    outputs: ["Output 1", "Output 2"]
  }
}
```

### Add a new public tab
1. Add nav button in the nav-bar (before the nav-divider):
```html
<button class="nav-tab" onclick="showTab('newtab',this)" data-zone="public">Tab Name</button>
```
2. Add section HTML:
```html
<div id="newtab" class="section">
  <div class="section-title">Title</div>
  <div class="section-sub">Subtitle</div>
  <!-- content -->
</div>
```

### Add a new protected tab
Same as above but add `class="nav-tab protected"` to the nav button.

### Connect Supabase
The intake form already has the structure for Supabase. To activate:
1. Create a Supabase project (or use existing)
2. Create tables matching the localStorage schemas (see ARCHITECTURE.md)
3. Add to the script:
```javascript
var SUPABASE_URL = 'https://your-project.supabase.co';
var SUPABASE_KEY = 'your-anon-key';
```
4. In `submitIntake()`, add after the localStorage save:
```javascript
fetch(SUPABASE_URL + '/rest/v1/restaurant_visits', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'apikey': SUPABASE_KEY,
    'Authorization': 'Bearer ' + SUPABASE_KEY
  },
  body: JSON.stringify(record)
});
```

---

## Design System Reference

### Colours
| Variable | Hex | Usage |
|----------|-----|-------|
| --gold | #c9a84c | Brand accent, highlights, CTAs |
| --red | #e05545 | Losses, leaks, warnings |
| --green | #4ade80 | Savings, positive, success |
| --blue | #60a5fa | Info, neutral, follow-up |
| --ink | #f0ede4 | Primary text on dark bg |
| --bg | #0a0a08 | Page background |
| --surface | #161614 | Card background |

### Typography
| Font | Weight | Usage |
|------|--------|-------|
| Syne | 800 | Headlines, titles, KPI numbers |
| Epilogue | 300–600 | Body, descriptions, form labels |
| DM Mono | 400–500 | Tags, labels, code-like elements |

### Key CSS Classes
| Class | Purpose |
|-------|---------|
| `.card` | Container with border + shadow |
| `.card-title` | Bold heading inside card |
| `.kpi` | Individual metric box |
| `.sc-tab` | Scenario/filter button |
| `.diag-card` | Accordion diagnostic category |
| `.diag-item` | Individual clickable diagnostic line |
| `.drill-panel` | Expanded drill-down content |
| `.form-input` | Text/number input field |
| `.form-submit` | Gold submit button |

---

## Testing Checklist

Before deploying any change, verify:

- [ ] Page loads without console errors (F12 → Console)
- [ ] Demo tab: venue chips clickable, KPIs populate, chart renders
- [ ] Sliders: moving sliders updates live profit numbers
- [ ] Unlock: entering `fe2025` reveals protected tabs
- [ ] Diagnostic: expanding a category shows items
- [ ] Drill-down: clicking any item shows detail panel
- [ ] Deep tree: clicking "Labour cost %" shows 3-branch forensic tree
- [ ] Intake form: submitting saves to localStorage (check Application → Local Storage)
- [ ] Pipeline: visit appears in table after submission
- [ ] Revenue tracker: logging payment updates progress bar
- [ ] Mobile: basic usability on phone-width screen

---

## Owner Contact

**Godfred Frimpong**
- Business: WorkMaster Group / The Food Economist
- Location: London, UK
- Prefers: Email-only communication, no phone/video
- Technical: Non-developer, uses Claude AI for all code changes
- Domain: thefoodeconomist.co.uk (Hostinger)
- GitHub: github.com/kfrem
