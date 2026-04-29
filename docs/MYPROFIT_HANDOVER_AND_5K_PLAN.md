# MyProfit / FoodEconomist Handover and £5K per Month Growth Plan

## 1. Current Project Position

This repository powers the MyProfit / FoodEconomist restaurant profit triage and diagnostic website.

The current live site is:

- `https://myprofit.thefoodeconomist.co.uk/`

The commercial objective is to turn the current restaurant profit calculator into a revenue system that can generate:

- one-off £79 written diagnostics
- monthly recurring profit monitoring
- partner/referral revenue
- proof dashboards that make the service easier to sell

The main target customer is an owner-managed UK restaurant, takeaway, caterer or food business that has messy figures, incomplete records, hidden small expenses, cash pressure, supplier cost movement, delivery platform charges, card fees, rent/rates pressure, energy costs, labour cost pressure and weak visibility before month end.

## 2. What Has Been Done

### 2.1 Repository and deployment structure

The GitHub repository is:

- `kfrem/foodeconomist-portal`

The working structure has been reorganised so that:

- `index.html` is the public MyProfit landing page and free triage tool.
- `portal.html` preserves the original deeper portal/full diagnostic system route.
- `sales-homepage-v2.html` remains as a previous sales-page version.
- `docs/` contains planning and handover documentation.
- `CLAUDE_HANDOVER.md` was added to guide Claude or another local coding agent.

The local project folder used by the owner is:

- `C:\Users\kfrem\OneDrive\CLIENTS\CLOSE COMPANIES\KAFS LTD\KAFS AUTOMATION\Coaching Business\Apps Dev\The Food Economist\myprofit`

The local and GitHub workflow that has been used is:

```powershell
git pull origin main
git status
git add .
git commit -m "clear description"
git push origin main
```

The live Hostinger/GitHub deployment has successfully shown updates from GitHub on the live website.

### 2.2 Homepage and sales funnel

The homepage was changed into a restaurant profit triage sales page.

It currently communicates:

- restaurants can use rough figures
- messy data is accepted
- food, labour, rent, delivery and hidden costs can damage profit
- the free triage gives warning signs
- the £79 diagnostic gives written clarity

The page includes:

- hero section
- free rough-data triage calculator
- custom extra cost entry
- £79 diagnostic offer
- referral/partner section
- contact section

### 2.3 Stripe payment link

A Stripe Payment Link was created and tested. It loads a £79 checkout page.

The public link inserted into `index.html` is:

```text
https://buy.stripe.com/00wbJ2dk80aNfwYcQF4ZG01
```

The JavaScript config contains:

```javascript
const CONFIG={contactEmail:'godfred@thefoodeconomist.co.uk',paymentLink:'https://buy.stripe.com/00wbJ2dk80aNfwYcQF4ZG01',intakeFormLink:'',whatsappNumber:'447939823988'};
```

The button `Request £79 Diagnostic` / diagnostic CTA routes to the Stripe payment link if `CONFIG.paymentLink` is present.

Important Stripe safety rule:

- Only public Stripe Payment Links may be placed in frontend HTML.
- No Stripe secret keys, API keys, webhook secrets, `.env` files, passwords or private credentials should ever be committed to GitHub.

### 2.4 Custom expense line upgrade

The calculator was upgraded so restaurants can add additional costs that do not fit the original simple fields.

Users can now add named expense lines such as:

- Cleaning
- Packaging
- Card fees
- Repairs
- Pest control
- Laundry
- Licences
- Marketing
- Owner drawings/cash taken out
- Other unknown costs

Each expense line supports:

- custom name
- amount
- period: weekly, monthly or one-off this month
- category dropdown

Categories currently include:

- Food / suppliers
- Labour / wages
- Rent / rates
- Energy / utilities
- Water
- Delivery / platform fees
- Packaging / disposables
- Cleaning / laundry
- Repairs / maintenance
- Insurance / licences
- Marketing / promotions
- Bank / card / finance fees
- Professional fees
- Owner drawings / cash taken out
- Other / unknown

The calculation now:

- converts additional costs into monthly values
- aggregates them by category
- adds relevant custom costs into food, labour, fixed costs or other costs
- separates owner drawings from operating profit
- updates operating profit, rough margin, cost pressure, risk and diagnostic issues

### 2.5 Live testing done

The live website was checked and confirmed to show the new MyProfit page at:

- `https://myprofit.thefoodeconomist.co.uk/`

The page displayed the updated message:

- `Small costs quietly destroy profit.`

This confirmed that the live site had updated from GitHub.

The local file was also opened from PowerShell using:

```powershell
.\index.html
```

The local file opened in the browser using a `file:///C:/...` address. This is local testing only.

The live customer test must always use:

```text
https://myprofit.thefoodeconomist.co.uk/
```

## 3. What Has Not Yet Been Completed

The following items are still outstanding:

1. The result output needs more attractive visual dashboard elements.
2. The homepage text needs readability polishing.
3. Proof-of-work / example dashboard sections need to be added.
4. Automated lead capture has not yet been implemented.
5. Automated email or WhatsApp follow-up has not yet been implemented.
6. The monthly recurring model has not yet been fully built into the user journey.
7. Payment success handling has not yet been connected to an intake form.
8. A real CRM or Google Sheet lead store has not yet been connected.
9. No backend exists yet; the site is currently static HTML/JavaScript.

## 4. Current Risk and Known Weaknesses

### 4.1 Static site limitation

The current system stores some triage data in browser `localStorage`. This is useful for temporary local behaviour but does not send the data to the owner automatically.

Therefore, if a user runs the triage but does not email/WhatsApp/pay, the owner may not receive the lead.

### 4.2 Lead capture gap

The system needs a proper lead capture mechanism. Options:

- Formspree
- Tally form
- Google Form
- Airtable form
- Supabase table
- Netlify/Vercel function
- Hostinger PHP endpoint

For speed, use Tally or Google Forms first. For long-term control, use Supabase or a backend endpoint.

### 4.3 Follow-up gap

There is no automated follow-up sequence yet.

Needed:

- email confirmation after triage
- payment confirmation / intake request
- reminder if user runs triage but does not pay
- monthly monitoring upsell after diagnostic

### 4.4 Proof gap

The site needs proof dashboards and example outputs showing what a customer receives.

Suggested proof examples:

- Example 1: Busy restaurant with hidden loss
- Example 2: Delivery sales with weak margin
- Example 3: Owner drawings causing cash pressure
- Example 4: Small costs consuming profit

Each proof should show:

- rough numbers
- chart / breakdown
- warning interpretation
- suggested action
- CTA to £79 diagnostic

## 5. Roadmap to Turn This into a £5K per Month System

### Target revenue maths

Simple path to £5K per month:

#### Option A: Diagnostic-heavy model

- 65 diagnostics per month at £79 = £5,135/month

This requires high volume and strong traffic.

#### Option B: Recurring model

- 20 clients at £99/month = £1,980/month
- 25 diagnostics at £79 = £1,975/month
- 10 setup/review calls at £99 = £990/month
- Total = £4,945/month

#### Option C: Partner-led model

- 10 referral partners each send 5 diagnostics/month = 50 diagnostics
- 50 diagnostics x £79 = £3,950/month
- 15 monthly monitoring clients x £99 = £1,485/month
- Total = £5,435/month

Recommended approach: Option C, because the owner does not want to do heavy cold selling.

## 6. Product Model to Build

### 6.1 Free product

Name:

- MyProfit Free Restaurant Profit Triage

Purpose:

- lead capture
- show risk
- create urgency
- prove usefulness

Free output should show:

- risk level
- estimated monthly profit range
- food cost pressure
- labour pressure
- prime cost pressure
- overhead pressure
- additional costs captured
- top hidden cost area
- records risk
- recommendation to pay for diagnostic

### 6.2 Entry paid product

Name:

- MyProfit 48-Hour Restaurant Profit Diagnostic

Price:

- £79

Deliverable:

- written PDF/report or email summary
- profit risk interpretation
- cost map
- top leakage areas
- accountant-ready category summary
- recommended actions
- invitation to monthly monitoring

### 6.3 Monthly recurring product

Name:

- MyProfit Monthly Profit Monitoring

Suggested pricing:

- Starter: £49/month
- Standard: £99/month
- Advisory: £199/month

#### Starter £49/month

- monthly category review
- cost pressure warning
- one email summary
- basic dashboard snapshot

#### Standard £99/month

- monthly review
- written summary
- hidden cost review
- owner drawings/cash pressure check
- 30-minute quarterly call

#### Advisory £199/month

- monthly review
- dashboard update
- WhatsApp support window
- pricing/cost action plan
- monthly 30-minute call

Recommended first public monthly offer:

- `Monthly Profit Monitoring from £49/month after the £79 diagnostic.`

## 7. Automated Lead Capture and Follow-Up Plan

### 7.1 Quick launch version

Use one of the following:

- Tally form
- Google Forms
- Airtable form

After the user runs the triage, show a button:

- `Send my figures for review`

This should send the owner to a form that captures:

- business name
- owner name
- email
- WhatsApp/mobile
- monthly sales estimate
- food/supplier spend
- wages
- rent/rates
- delivery/platform costs
- extra expense categories
- main worry
- permission to contact

### 7.2 Payment success flow

After Stripe payment, redirect to:

- `/intake.html` or an external intake form

The intake form should say:

`Thank you for purchasing the £79 diagnostic. Please send the figures you have. Rough data, screenshots and notes are acceptable.`

Stripe Payment Link should be configured with a success URL.

### 7.3 Email follow-up sequence

Suggested sequence:

#### Email 1: Immediately after triage

Subject:

- `Your restaurant profit triage is only the beginning`

Message:

- confirms rough figures are accepted
- explains warning signs
- invites £79 diagnostic

#### Email 2: 24 hours later

Subject:

- `Small costs do not wait until month end`

Message:

- shows example of packaging, cleaning and card fees damaging profit
- CTA to £79 diagnostic

#### Email 3: 72 hours later

Subject:

- `Would cleaner figures help your accountant or your own records?`

Message:

- emphasises accountant-ready categories
- CTA to diagnostic

#### Email 4: After paid diagnostic

Subject:

- `Keep this under control monthly`

Message:

- upsell monthly monitoring from £49/month

## 8. Proof Dashboards That Sell Themselves

Add a section called:

- `Example Profit Warnings`

Each proof card should show a mini-dashboard.

### Proof 1: Busy but leaking

Inputs:

- Sales: £32,000/month
- Food: £11,500
- Wages: £10,000
- Rent/rates: £5,000
- Hidden small costs: £3,200

Output:

- Operating profit before small costs may look acceptable
- Small costs turn it into pressure
- Recommendation: check suppliers, packaging, card fees, cleaning, delivery deductions

### Proof 2: Delivery app illusion

Inputs:

- Delivery sales look strong
- Platform fees and packaging reduce margin

Output:

- sales volume may be hiding weak contribution
- recommendation: test delivery menu pricing and commission impact

### Proof 3: Owner drawings pressure

Inputs:

- restaurant appears profitable before owner cash taken out
- owner drawings exceed safe cash level

Output:

- business may not support owner consistently
- recommendation: separate operating profit from owner drawings

### Proof 4: Accountant-ready clean-up

Before:

- WhatsApp notes
- bank payments
- card fees
- supplier invoices
- cash drawings
- unknown expenses

After:

- food/suppliers
- wages
- rent/rates
- utilities
- delivery/platform fees
- packaging
- repairs/maintenance
- card/finance fees
- owner drawings

Message:

- `Messy figures become cleaner categories for better owner decisions and easier accountant conversations.`

## 9. Recommended Next Build Tasks for AI / Developer

### Task 1: Improve readability

- Reduce hero headline size.
- Make text shorter and easier to scan.
- Use more bullets.
- Keep black/gold premium look.

### Task 2: Add visual dashboard bars

In the result panel add visual bars for:

- food cost %
- labour %
- prime cost %
- overhead %
- hidden small costs as % of sales

These should update after the user runs the triage.

### Task 3: Add proof dashboard section

Add 3 to 4 proof cards with sample figures and mini visual bars.

### Task 4: Add monthly monitoring section

Add a section after the £79 diagnostic:

- headline: `Monthly Profit Monitoring`
- price: `From £49/month`
- CTA to WhatsApp or enquiry form

### Task 5: Add lead capture

Short-term:

- connect Tally / Google Form / Airtable

Long-term:

- add Supabase lead table
- store triage results securely
- send email notification to owner

### Task 6: Add intake page

Create:

- `intake.html`

Purpose:

- after payment, user submits full figures, uploads screenshots or explains their problem

### Task 7: Add success page

Create:

- `success.html`

Purpose:

- Stripe redirects customer after payment
- thanks them
- tells them what happens next
- sends them to intake form

### Task 8: Add email automation

Use:

- MailerLite
- Brevo
- Mailchimp
- ConvertKit
- Zapier/Make
- n8n

Minimum automation:

- free triage lead -> email reminder
- paid diagnostic -> intake email
- diagnostic delivered -> monthly monitoring upsell

## 10. Launch Today Checklist

Minimum launch checklist:

1. Live site opens at `https://myprofit.thefoodeconomist.co.uk/`.
2. Calculator loads.
3. Extra expenses can be added.
4. Triage result updates.
5. `Request £79 Diagnostic` opens Stripe checkout.
6. Stripe checkout public name should show `The Food Economist` or similar, not confusing unrelated branding.
7. Stripe statement descriptor should be recognisable, e.g. `FOODECONOMIST`.
8. After payment, user must know what to do next.
9. Add at least one WhatsApp/contact route.
10. Start with 5 restaurant conversations.

## 11. First 48-Hour Sales Plan

Do not begin with ads.

Start with warm/direct outreach to:

- restaurants already known to the owner
- bookkeepers
- accountants
- food suppliers
- POS installers
- energy brokers
- delivery consultants
- restaurant networks

Message:

`I have built a quick restaurant profit triage that accepts messy figures and shows whether food cost, wages, rent, delivery fees and small expenses may be damaging profit. It is designed for owners who do not have perfect accounts. Would you be willing to test it and tell me whether the £79 written diagnostic is worth offering to restaurants like yours?`

Partner message:

`I have built a restaurant profit triage tool for owner-managed restaurants with messy figures. It helps them see food cost, labour, overhead and hidden small cost pressure before month end. If you know restaurants struggling with cash visibility, I can offer a £79 diagnostic and pay a £20 referral fee for paid introductions.`

## 12. Important Git and Local Workflow

To update local from GitHub:

```powershell
cd "C:\Users\kfrem\OneDrive\CLIENTS\CLOSE COMPANIES\KAFS LTD\KAFS AUTOMATION\Coaching Business\Apps Dev\The Food Economist\myprofit"
git pull origin main
```

To commit local changes:

```powershell
git status
git add .
git commit -m "Describe the change"
git push origin main
```

Do not type multiple commands on one line.

Correct:

```powershell
git pull origin main
```

Wrong:

```powershell
git push origin maingit pull origin main
```

## 13. What A New AI / Developer Should Understand

This is not merely an HTML calculator.

It is intended to become:

- a lead magnet
- a diagnostic sales funnel
- a restaurant profit advisory product
- a monthly recurring monitoring service
- a partner-referral business

The winning proposition is:

`Turn messy restaurant numbers into a profit warning, cost map and cleaner accountant-ready categories before the month gets worse.`

The technical build must protect the original portal and avoid exposing secrets.

Do not remove:

- Stripe public payment link unless replacing it with a better payment route
- custom expense engine
- `portal.html`
- docs/handovers

## 14. Immediate Next Recommendation

The fastest practical next step is not another large redesign.

It is:

1. Add `success.html`.
2. Add `intake.html` or link to a Tally/Google Form.
3. Add proof dashboard section.
4. Add monthly monitoring CTA.
5. Start selling to 5 real restaurants.

The site is already strong enough to test. Further polish should be driven by real user feedback.
