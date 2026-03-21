# April 17, 2026 Crowdfunding Launch Checklist

**Launch time:** April 17, 2026 at 12:00 PM EDT
**Campaign:** Sing Until Nobody's Gone — GoFundMe
**Website:** kikistop.github.io/sing-until-nobodys-gone

---

## Pre-Launch (by April 14) — Board Actions Required

### GoFundMe Page
- [ ] GoFundMe page created (see SUN-293 for step-by-step instructions)
- [ ] Page set to **Unlisted** until launch (not publicly searchable)
- [ ] Goal amount confirmed
- [ ] Cover image/video uploaded
- [ ] Beneficiary bank account verified for withdrawals
- [ ] FA fiscal sponsorship status confirmed (affects tax-deductible language)
- [ ] Inner-circle early backer list ready (15–20 contacts for April 3 soft launch)

### Website Activation (Engineering — 5 min once GoFundMe URL is known)
- [ ] Replace `GOFUNDME_URL_HERE` in `index.html` (2 occurrences — banner + gofundme-section)
- [ ] Replace `GOFUNDME_URL_HERE` in `night-owl.html` (1 occurrence)
- [ ] Change `display: none` → `display: block` on `#gofundme-section` in `index.html`
- [ ] Merge PR #1 (`gofundme-activate`) → GitHub Pages auto-deploys in ~60 seconds

---

## UTM Link Verification

After GoFundMe URL is live, verify all 6 UTM-tracked links load the GoFundMe page:

| # | Source | UTM Parameters | Location |
|---|--------|----------------|----------|
| 1 | `website/banner` | `utm_source=website&utm_medium=banner&utm_campaign=gofundme-launch` | `index.html` banner |
| 2 | `night-owl-page/website` | `utm_source=night-owl-page&utm_medium=website&utm_campaign=gofundme-launch` | `night-owl.html` CTA |
| 3 | `email/newsletter` | `utm_source=email&utm_medium=newsletter&utm_campaign=gofundme-launch` | Board email blast |
| 4 | `instagram/social` | `utm_source=instagram&utm_medium=social&utm_campaign=gofundme-launch` | Instagram post |
| 5 | `tiktok/social` | `utm_source=tiktok&utm_medium=social&utm_campaign=gofundme-launch` | TikTok post |
| 6 | `twitter/social` | `utm_source=twitter&utm_medium=social&utm_campaign=gofundme-launch` | Twitter/X post |

**Verification steps:**
1. Click each UTM link from the list above (or construct them by appending params to the GoFundMe URL)
2. Confirm GoFundMe page loads correctly
3. Check GoFundMe campaign dashboard → "How did people find you?" to confirm UTM tracking is recording

---

## Donation Tracking Setup

### Option A — GoFundMe built-in (recommended)
GoFundMe's dashboard shows:
- Total raised / goal
- Number of donors
- Recent donations
- Referral source breakdown (if UTM params are tracked by GoFundMe)

Export: GoFundMe Dashboard → "Supporters" → Export CSV

### Option B — Google Sheets manual tracker
If board wants a separate tracking sheet, create with these columns:

```
Date | Donor Name | Amount | Platform | UTM Source | Notes
```

Weekly update from GoFundMe CSV export. See `GOFUNDME_WEEKLY_REPORT_TEMPLATE.md` in sunlog repo for the full weekly report format.

### Option C — SunLog crowdfunding stats endpoint (if deployed)
Once SunLog is live: `GET /api/crowdfunding-stats` returns `{ pledged, goal, backerCount }`.
The crowdfunding.html progress bar auto-fetches this every 60 seconds.

---

## Launch Day Checklist (April 17 — 12:00 PM EDT)

### T-60 min (11:00 AM)
- [ ] GoFundMe page switched from **Unlisted** to **Public**
- [ ] All UTM links verified working
- [ ] Social media posts drafted and ready to publish at noon

### T-0 (12:00 PM EDT)
- [ ] Post all social media simultaneously (Twitter/X, Instagram, TikTok)
- [ ] Send email newsletter to full list
- [ ] Post in WhatsApp/Signal groups

### T+30 min
- [ ] Verify GoFundMe page is loading for external users (test from incognito window)
- [ ] Check first donations are appearing in dashboard
- [ ] Monitor for any broken links or errors

### T+24 hours
- [ ] First daily donation report (use GOFUNDME_WEEKLY_REPORT_TEMPLATE.md format)
- [ ] Share update with inner-circle backers

---

## SunLog Dependency (if deployed by April 17)

If SunLog Railway deploy completes before April 17:
1. Update `SUNLOG_API` in `signup.html` from `sunlog.onrender.com` to new Railway URL
2. Update `SUNLOG_API` in `crowdfunding.html` (same constant)
3. Update `SUNLOG_API` in `early-access.html`
4. Run load test: `npm run loadtest` in sunlog repo (see LOAD_TESTING.md)
5. Confirm `/api/crowdfunding-stats` endpoint returns correct data

If SunLog is NOT deployed by April 17:
- Email capture on crowdfunding.html queues to localStorage and retries on reconnect
- Email capture on signup.html shows Google Form backup link (set `GOOGLE_FORM_BACKUP_URL`)
- All other pages function normally (static GitHub Pages)

---

**Related:** [SUN-293](/SUN/issues/SUN-293) (GoFundMe), [SUN-48](/SUN/issues/SUN-48) (deploy), [SUN-305](/SUN/issues/SUN-305) (soft launch)
