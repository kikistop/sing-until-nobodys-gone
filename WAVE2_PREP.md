# Wave 2 RSVP Integration Prep — SUN-251

**Wave 1 Close:** March 22, 2026 (TOMORROW)
**Wave 2 Open:** April 1, 2026
**Current registered singers:** 247

---

## Immediate Actions (Before March 22)

### 1. Toggle Wave 2 Banner (DO NOT commit yet — board approval needed)

The banner is staged in `index.html` and ready to activate. To show it:

```html
<!-- In index.html, change this: -->
#wave2-banner { display: none; }
/* TO: */
#wave2-banner { display: block; }
```

**Update banner text before toggling:**
```html
<!-- Current text: "240+ singers already in the pipeline" -->
<!-- Change to: "247 singers already signed up" -->
```

Board action: Approve banner toggle for April 1 (Wave 2 open date), not today.

### 2. Wave 1 Close Announcement Copy

Add this section to index.html above the existing "sign up" CTA between March 22–March 31:

```html
<!-- WAVE 1 CLOSE BANNER — show March 22–31 only -->
<div style="background: linear-gradient(90deg, #1a1a2e, #16213e); border: 1px solid rgba(255,45,120,0.3); border-radius: 12px; padding: 20px 24px; margin: 24px 0; text-align: center;">
  <div style="font-size: 0.8rem; font-weight: 700; color: var(--pink); text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 8px;">Wave 1 RSVP Closed</div>
  <p style="color: var(--gray-light); margin: 0 0 12px;">Wave 1 registration has closed with <strong style="color: var(--white);">247 singers</strong> in the pipeline.
  <strong style="color: var(--pink);">Wave 2 opens April 1.</strong></p>
  <a href="signup.html?utm_source=wave1-close&utm_medium=website&utm_campaign=wave2" style="display:inline-block; background: var(--pink); color: #fff; padding: 10px 24px; border-radius: 100px; font-weight: 700; text-decoration: none; font-size: 0.9rem;">Join the Wave 2 Waitlist →</a>
</div>
```

### 3. Night Owl Club Section — Number Update

In `index.html`, line 163 shows `240+`. Update to `247+` when the Wave 1 close banner goes live.

In `signup.html`, line 39 shows `247`. This is already current — no change needed.

---

## Wave 2 Registration Flow Plan

### What Changes in Wave 2

| Item | Wave 1 | Wave 2 |
|------|--------|--------|
| Sign-up URL | `signup.html` | `signup.html` (same form, new wave tag) |
| UTM campaign | `wave1` | `wave2` |
| Social proof copy | "240+ singers" | "247+ singers — join the next wave" |
| Urgency copy | "Registration closes May 2026" | "Wave 2 spots limited — next close April 30" |
| Banner | Hidden | Active (April 1) |
| Email followup | Standard confirmation | Wave 2 confirmation with "you're in the next wave" copy |

### Signup.html Updates for Wave 2

1. **Update social proof bar** (line 39): Change `247` to live dynamic count (fetch from `/api/analytics` if SunLog is live, or manually update)
2. **Update urgency pill**: Change "Registration closes May 2026" → "Wave 2 closes April 30"
3. **Update form submission UTM**: Add `wave=2` parameter to form payload for SunLog tracking
4. **Update confirmation page** (`thank-you.html`): Add "You're in Wave 2 — event starts June 12" messaging

### Form Field Additions for Wave 2 (Optional)

Consider adding to signup form for Wave 2:
- `rsvp_wave` hidden field: value `"2"` (tracked in SunLog for wave analytics)
- `referred_by` field: "How did you hear about Wave 2?" (capture word-of-mouth from Wave 1 singers)

### SunLog API Support

Wave tracking is supported via the `utm_campaign` field already stored in `/api/register`. Wave 2 registrations should use:
- `utm_campaign: "wave2"` OR a dedicated `wave` field added to registration payload

Analytics query to check wave breakdown:
```bash
curl -s https://sunlog.onrender.com/api/analytics
# Returns byBlock, total — add wave breakdown if needed
```

---

## Night Owl Club Updates

### Current Numbers (March 20)
- Total registered: 247 singers
- Night Owl (overnight, 10pm–7am): tracked via `preferred_block = 'night_owl'` in SunLog
- Night Owl number visible in `night-owl.html` (check current count before updating)

### Staged Updates for Wave 2 Launch (April 1)

In `night-owl.html`, update the social proof section with current Night Owl count from SunLog:
```bash
curl -s https://sunlog.onrender.com/api/analytics
# Check night_owl count in byBlock response
```

Add to `night-owl.html` above the CTA section:
```html
<div style="text-align:center; margin: 32px 0;">
  <div style="font-size: 2rem; font-weight: 900; color: var(--gold);">[NIGHT_OWL_COUNT]</div>
  <div style="color: var(--gray-light); font-size: 0.9rem;">Night Owls already committed</div>
</div>
```
Replace `[NIGHT_OWL_COUNT]` with actual count from SunLog analytics before committing.

---

## Wave 2 Announcement Email Template

**Subject:** Wave 2 is open — 247 singers and counting 🎤

```
Hey [first_name],

Wave 1 RSVP officially closed with 247 singers in the pipeline. We're blown away.

Wave 2 is now open. If you know someone who missed Wave 1, now's their chance.

[SIGN UP FOR WAVE 2 → link]

The record attempt starts June 12 in Times Square. 38 days. 912 hours. Let's make history.

— The SUN Team
```

UTM: `utm_source=email&utm_medium=newsletter&utm_campaign=wave2-launch`

---

## Implementation Checklist

### March 22 (Wave 1 Close)
- [ ] Manually confirm final Wave 1 count from SunLog (or Google Forms if SunLog still offline)
- [ ] Update all "240+" references to final count in index.html
- [ ] Commit "Wave 1 close" static copy (do NOT toggle Wave 2 banner yet)

### April 1 (Wave 2 Open)
- [ ] Toggle Wave 2 banner: `display: none` → `display: block` in index.html
- [ ] Update banner singer count to latest number
- [ ] Update signup.html urgency pill: "Wave 2 closes April 30"
- [ ] Update Night Owl Club count on night-owl.html
- [ ] Send Wave 2 launch email to all 247+ contacts
- [ ] Post social media announcement (Instagram, TikTok, Twitter)

### April 30 (Wave 2 Close)
- [ ] Hide Wave 2 banner
- [ ] Show "Registration closed — event is June 12" static message
- [ ] Send final confirmation to all registered singers

---

*Prep doc created March 20, 2026 (SUN-251). Wave 1 closes March 22. Wave 2 opens April 1. Relates to SUN-48 (SunLog live = real-time counts), SUN-87 (website improvements).*
