# Deployment Guide — GitHub → Hostinger Auto-Deploy

## Overview

Every time you push a change to GitHub, Hostinger automatically pulls the latest version. No manual file uploads. No FTP. No cPanel file manager.

**Cost: £0** (uses free GitHub + existing Hostinger plan)

---

## One-Time Setup (15 minutes)

### Step 1: Create the GitHub Repository

1. Go to https://github.com/new
2. Repository name: `foodeconomist-portal`
3. Set to **Private** (your code, your business)
4. Click "Create repository"
5. Follow the push instructions below

### Step 2: Push the Code

From your local machine (or ask Claude to prepare the commands):

```bash
cd /path/to/foodeconomist-portal
git init
git add .
git commit -m "Initial portal deployment"
git branch -M main
git remote add origin https://github.com/kfrem/foodeconomist-portal.git
git push -u origin main
```

### Step 3: Connect Hostinger to GitHub

1. Log into Hostinger → hPanel
2. Go to **Websites** → select `thefoodeconomist.co.uk`
3. Go to **Advanced** → **Git**
4. Click **Connect Git Repository**
5. Enter repository URL: `https://github.com/kfrem/foodeconomist-portal.git`
6. Branch: `main`
7. Directory: `/public_html/myprofit` (or wherever your subdomain points)
8. Click **Connect**
9. Hostinger will ask you to authenticate with GitHub — follow the OAuth flow

### Step 4: Set Up Auto-Deploy (Webhook)

1. In Hostinger Git settings, find the **Webhook URL** (it looks like `https://api.hostinger.com/git/webhook/xxxxx`)
2. Go to your GitHub repo → **Settings** → **Webhooks** → **Add webhook**
3. Payload URL: paste the Hostinger webhook URL
4. Content type: `application/json`
5. Events: **Just the push event**
6. Click **Add webhook**

Now every `git push` automatically triggers Hostinger to pull the latest code.

---

## Alternative: Hostinger Git Without Webhook

If webhooks are not available on your Hostinger plan:

1. Connect the repo as above
2. In hPanel → Git, click **Pull** manually after each push
3. This still saves the upload/download/FTP cycle — just one button click

---

## Alternative: GitHub Pages (Free Hosting)

If you want a completely free secondary deployment:

1. In your GitHub repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Your portal will be live at: `https://kfrem.github.io/foodeconomist-portal/`

This gives you a free backup URL while keeping the primary on Hostinger.

---

## Daily Workflow After Setup

### When Claude Makes Changes:
1. Claude generates an updated `index.html`
2. You download it
3. Replace the file in your local repo folder
4. Run:
```bash
git add index.html
git commit -m "Update: [description of change]"
git push
```
5. Hostinger auto-deploys within 30–60 seconds
6. Refresh your browser — changes are live

### Even Simpler: GitHub Web Editor
1. Go to https://github.com/kfrem/foodeconomist-portal
2. Click `index.html`
3. Click the pencil icon (Edit)
4. Paste the entire new file content
5. Click **Commit changes**
6. Hostinger auto-deploys

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Changes not appearing | Clear browser cache (Ctrl+Shift+R) |
| Hostinger not pulling | Go to hPanel → Git → click Pull manually |
| Webhook not firing | Check GitHub → Settings → Webhooks → Recent Deliveries |
| 404 on subdomain | Check Hostinger subdomain points to correct directory |
| Git authentication error | Re-connect GitHub in Hostinger hPanel |

---

## File Naming

The portal file MUST be named `index.html` (not `portal.html` or `foodeconomist-portal.html`). This is because Hostinger (and all web servers) serve `index.html` by default when someone visits a directory URL.
