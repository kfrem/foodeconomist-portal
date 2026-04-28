# Claude / Local Agent Handover — MyProfit FoodEconomist Portal

## Current Purpose

This repository powers the MyProfit / FoodEconomist restaurant profit intelligence website.

The commercial goal is to turn the site into a sales funnel for a paid restaurant profit diagnostic offer, without destroying the original diagnostic portal that took months to build.

## Current Commercial Offer

Primary offer:

- **Free Profit Triage** for restaurants and food businesses using rough figures.
- **£79 48-Hour Restaurant Profit Diagnostic** as the first paid product.
- Future upsell: monthly profit monitoring / advisory support.

The intended buyer is an owner-managed restaurant, caterer, takeaway, food business or a referral partner such as a bookkeeper, accountant, supplier, POS installer, energy broker, insurance broker or restaurant adviser.

## Key Strategic Decision

We chose **Option A**:

- `index.html` should become the public sales homepage.
- `portal.html` should hold the full original diagnostic portal / protected system.
- `sales-homepage-v2.html` is the latest public sales page / rough-data triage engine.

## Current Important Files

### `index.html`

Currently the original full portal in the local working folder unless it has already been swapped locally.

This file contains the deeper diagnostic system, protected tabs, charts, diagnostic cards, internal tools and the original portal structure.

Do not overwrite this file casually.

### `sales-homepage-v2.html`

This is the new public sales homepage and lead magnet.

It contains the upgraded **rough-data restaurant profit triage engine**.

This page accepts imperfect inputs such as:

- daily / weekly / monthly sales estimate
- trading days per week
- weekly or monthly supplier spend
- weekly or monthly wages
- weekly or monthly rent/fixed overheads
- delivery/platform fees or other costs
- main worry / pain point

It outputs:

- risk classification
- estimated monthly profit range
- confidence level
- rough margin
- food cost pressure
- labour pressure
- prime cost pressure
- fixed overhead pressure
- diagnostic issue list
- call to action for the £79 diagnostic

The key positioning is: **not a spreadsheet calculator, but a business triage tool for messy restaurant data**.

### `portal.html`

This is intended to become the preserved full original diagnostic portal.

If still a placeholder, copy the full existing `index.html` into it locally before replacing `index.html` with the sales page.

Local PowerShell command:

```powershell
Copy-Item index.html portal.html -Force
```

Then make sales page the homepage:

```powershell
Copy-Item sales-homepage-v2.html index.html -Force
```

Then check:

```powershell
git status
```

Commit and push:

```powershell
git add .
git commit -m "Make sales triage page public homepage and preserve portal"
git push origin main
```

## Safety Rules

1. Do not commit Stripe secret keys, API keys, webhook secrets, passwords, `.env` files or private credentials.
2. A public Stripe Payment Link is safe to place in frontend HTML.
3. If using Stripe API keys later, move payment logic to a backend or serverless endpoint and keep secrets outside GitHub.
4. Treat GitHub as the source of truth.
5. Before local work, run:

```powershell
git fetch origin
git pull origin main
git status
```

6. Do not push old local files over newer GitHub changes.

## Recent Work Completed

1. Built `sales-homepage-v2.html` as a conversion-focused sales homepage.
2. Added real contact details:
   - Email: `godfred@thefoodeconomist.co.uk`
   - WhatsApp: `+44 7939 823988`
3. Upgraded the free calculator into a rough-data diagnostic triage engine.
4. Created `docs/SALES-AUTOMATION-PLAN.md`.
5. Created GitHub issues documenting:
   - rough-data lead magnet improvement
   - local/GitHub sync workflow
   - Stripe safety workflow
   - Option 1 GitHub-as-source-of-truth workflow
6. Began the restructure towards:
   - `index.html` = public sales page
   - `portal.html` = full protected diagnostic portal

## Recommended Next Step

Complete the local file swap if not done already:

```powershell
Copy-Item index.html portal.html -Force
Copy-Item sales-homepage-v2.html index.html -Force
git status
```

Then commit and push.

After that, create a Stripe Payment Link for:

- Product: MyProfit 48-Hour Restaurant Profit Diagnostic
- Price: £79
- Type: One-time payment
- Currency: GBP

Then insert the public payment link into this JavaScript config in `index.html`:

```javascript
const CONFIG={contactEmail:'godfred@thefoodeconomist.co.uk',paymentLink:'',intakeFormLink:'',whatsappNumber:'447939823988'};
```

Replace the empty `paymentLink:''` with the Stripe payment link.

## Positioning Reminder

The public page must not look like a basic Excel calculator.

The selling point is:

> Many restaurant owners have messy figures, not perfect accounts. MyProfit uses rough data to reveal whether there is enough risk to justify a proper diagnostic.

Free triage creates concern. The £79 diagnostic sells clarity.

## Do Not Destroy

The original full portal and diagnostic framework must be preserved. If unsure, create a backup branch before major changes.

Suggested branch for experiments:

```powershell
git checkout -b safe-experiment
```

