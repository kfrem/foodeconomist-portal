# Roadmap — Remaining Work (~55%)

## Current State: ~45% Complete

### What Works Now ✅
- [x] Unified single-file portal with dark editorial design
- [x] Three-tier access system (public / protected / deep diagnostic)
- [x] Public demo with 6 venue types, KPIs, charts, P&L, scenario sliders
- [x] Energy audit calculator
- [x] Supplier network grid
- [x] Contact page with WhatsApp/Telegram
- [x] Pricing page (flexible — no fixed fees shown)
- [x] Full diagnostic framework (10 categories, 180 line items)
- [x] Venue filtering with dynamic category labels
- [x] 5 deep forensic drill-down trees (Labour, Food Cost, Energy, Menu, Cash Flow)
- [x] 40+ bespoke standard drill-down items with 5-panel detail
- [x] Pattern-matching fallback for remaining 135 items
- [x] Multi-venue flowchart (Process Map)
- [x] Proof of Loss sample document
- [x] 48hr Snapshot process guide
- [x] Scripts and objection handling
- [x] Client acquisition strategy
- [x] 4-week plan to £5,000
- [x] Enhanced intake form (15+ fields)
- [x] Pipeline/CRM with status filtering and CSV export
- [x] £5K revenue tracker with payment logger
- [x] Message templates with copy buttons
- [x] GitHub repo with documentation

---

## Phase 2: Deep Diagnostic Completion (Priority: HIGH)

### 2A. Build remaining 5 deep forensic trees
**Effort: 3–4 hours | Impact: Critical for premium perception**

Build deep trees (same depth as Labour tree) for:
- [ ] **Premises, Rates & Occupancy** — Rateable value challenges, relief claims, lease negotiations, service charge audits
- [ ] **Delivery Platforms & Technology** — Commission structures, menu repricing, own-website ordering, EPOS optimisation
- [ ] **Finance, Tax & Compliance** — VAT scheme comparison, corporation tax, loan structures, HMRC compliance
- [ ] **Capacity & Revenue Optimisation** — RevPASH analysis, dead trading hours, seasonal planning, cover count trends
- [ ] **Marketing & Retention** — Google Business Profile audit, review response ROI, loyalty systems, repeat customer tracking

### 2B. Upgrade remaining 135 standard drill-down items to bespoke content
**Effort: 8–10 hours | Impact: High — every click should feel crafted**

Currently these use the pattern matcher (getDrillDown) which generates intelligent but generic content. Each should have hand-written explain/check/loss/fix/time content specific to the restaurant industry.

Priority order:
1. Items in Category 04 (Premises) — highest £ impact for clients
2. Items in Category 05 (Delivery) — most common pain point
3. Items in Category 06 (Finance) — highest credibility builder
4. Items in Category 07 (Menu) — most actionable for owners
5. Remaining categories

### 2C. Add data collection questionnaire layer
**Effort: 4–6 hours | Impact: Critical for actual service delivery**

For each of the 180 diagnostic items, define the specific questions that need to be asked to gather real data. This becomes the foundation for the client-facing data collection system.

Structure per item:
```
{
  questions: [
    { q: "What is your current food cost percentage?", type: "number", unit: "%" },
    { q: "When did you last get competing supplier quotes?", type: "select", options: ["Never","6+ months","3-6 months","Recently"] },
  ],
  documents_needed: ["Last 3 months supplier invoices", "Current menu with prices"],
  estimated_time: "15 minutes"
}
```

---

## Phase 3: Supabase Backend Integration (Priority: HIGH)

### 3A. Move CRM data to Supabase
**Effort: 3–4 hours | Impact: Critical — enables multi-device access**

- [ ] Create `restaurant_visits` table in Supabase (matches localStorage schema)
- [ ] Create `payments` table
- [ ] Modify `submitIntake()` to POST to Supabase REST API
- [ ] Modify `logPayment()` to POST to Supabase
- [ ] Add data loading on page init (fetch from Supabase, fallback to localStorage)
- [ ] Supabase credentials: use existing connected account

### 3B. Client data collection portal
**Effort: 6–8 hours | Impact: High — this is how you actually deliver the service**

Separate HTML page (e.g., `intake.thefoodeconomist.co.uk`) where:
- Client receives a unique link after booking a snapshot
- They fill in questionnaire sections relevant to their venue type
- Data saves to Supabase
- Godfred can view submissions in the portal's Pipeline tab
- Auto-generates a preliminary diagnostic from submitted data

### 3C. Report generation
**Effort: 4–6 hours | Impact: High — automates the 48hr snapshot delivery**

- [ ] Generate HTML/PDF report from client's submitted data + diagnostic findings
- [ ] Auto-populate Proof of Loss template with real client numbers
- [ ] Branded output with FoodEconomist design system
- [ ] Deliverable via email link or WhatsApp

---

## Phase 4: Public-Facing Polish (Priority: MEDIUM)

### 4A. Replace placeholder content
- [ ] Replace WhatsApp number `447700000000` with real number
- [ ] Add real testimonials/case studies (once first clients complete)
- [ ] Add Google Analytics or Plausible tracking
- [ ] Add meta tags for SEO (title, description, OG tags)
- [ ] Add favicon

### 4B. Mobile optimisation
- [ ] Test and fix all tabs on mobile (especially diagnostic drill-down)
- [ ] Ensure intake form is fully usable on phone
- [ ] Test scenario sliders on touch devices
- [ ] Hamburger menu for mobile nav (currently horizontal scroll)

### 4C. Additional public content
- [ ] Add "How It Works" visual process (for people who don't click Pricing)
- [ ] Add venue-specific landing sections ("For Indian Restaurants", "For Coffee Shops")
- [ ] Add blog/insights section (positions Godfred as expert)

---

## Phase 5: Automation & Scale (Priority: LOWER — after £5K achieved)

### 5A. Email/WhatsApp automation
- [ ] Auto-send follow-up messages at scheduled dates
- [ ] Integration with WhatsApp Business API (or Twilio)
- [ ] Automated appointment booking (Calendly or Cal.com embed)

### 5B. Client dashboard
- [ ] Each client gets a login to see their diagnostic progress
- [ ] Monthly metrics tracking with visual progress
- [ ] Savings achieved vs baseline comparison

### 5C. Multi-consultant scaling
- [ ] Role-based access (admin vs consultant)
- [ ] Consultant performance tracking
- [ ] Client assignment and handoff

---

## Effort Summary

| Phase | Effort | Priority | Revenue Impact |
|-------|--------|----------|----------------|
| 2A: 5 more deep trees | 3–4 hrs | HIGH | Converts prospects to clients |
| 2B: 135 bespoke items | 8–10 hrs | HIGH | Premium perception |
| 2C: Questionnaire layer | 4–6 hrs | HIGH | Enables service delivery |
| 3A: Supabase CRM | 3–4 hrs | HIGH | Multi-device, data safety |
| 3B: Client data portal | 6–8 hrs | HIGH | Automates data collection |
| 3C: Report generation | 4–6 hrs | HIGH | Automates delivery |
| 4A: Placeholder fixes | 1–2 hrs | MEDIUM | Professionalism |
| 4B: Mobile polish | 2–3 hrs | MEDIUM | Accessibility |
| 4C: Extra content | 3–4 hrs | MEDIUM | SEO & conversion |
| 5A–C: Automation | 10–15 hrs | LOWER | Scale beyond £5K/month |

**Total remaining: ~45–60 hours of development**
