# Automation Audit — Service Delivery Runbook

**Price:** $199 flat | **Turnaround:** 48 hours | **Format:** Loom video + written report

---

## 1. Intake

### What to Ask (Tally Form)

1. **Your name and store/business URL**
2. **Platform** — Zapier, Make (Integromat), or both?
3. **Access method** — Which do you prefer?
   - Option A: Read-only viewer access (Zapier: share via team invite with Viewer role; Make: share org with Viewer)
   - Option B: Screen recording of your dashboard (Loom or similar — record yourself scrolling through your zaps/scenarios)
4. **How many active zaps/scenarios do you have?** (rough count)
5. **Current monthly platform cost** (approximate — helps estimate savings)
6. **Top 3 workflows you want me to focus on** (describe briefly)
7. **Biggest pain point** — What's breaking, slow, or feeling clunky?
8. **Any specific outcome you want?** (e.g., reduce task usage, fix errors, simplify maintenance)

### Access Security Note (send to client on booking)

> "For Zapier: add me as a Viewer (Settings > Members). For Make: share the Organization with Viewer role. Viewer access is read-only — I cannot run, edit, or delete anything. Alternatively, just send a screen recording of your scenario list and I'll work from that."

---

## 2. Audit Process (60 minutes)

Work through each zap/scenario systematically. Allocate ~5 min per workflow for standard accounts (adjust for large orgs).

### Per-Workflow Checklist

**Error Rate (last 30 days)**
- [ ] Any errors in the task history? Note frequency and type (auth, timeout, data mismatch)
- [ ] Is there an error handler (Make) or filter fallback (Zapier)?
- [ ] Are errors silent — no notification to the owner?

**Step Count & Simplification**
- [ ] Can any steps be merged? (e.g., two formatter steps → one)
- [ ] Are there redundant lookups? (same record fetched multiple times)
- [ ] Any steps that do nothing observable? (logging to a dead end, updates that don't change data)

**Trigger Efficiency**
- [ ] Is a polling trigger being used where a webhook is available?
  - Polling burns task usage every interval even when nothing changed
  - Zapier: most major apps (Shopify, Stripe, Gmail) support instant triggers — use them
  - Make: prefer webhooks over scheduled triggers for event-driven flows
- [ ] Is the poll interval set unnecessarily short? (e.g., every 5 min when hourly is fine)

**Data Transformation Redundancy**
- [ ] Are values being formatted/parsed that arrive already in the right shape?
- [ ] Any unnecessary Array > String > Array round-trips?
- [ ] Duplicate lookups — same ID fetched in two separate steps?

**Common Issues Checklist**
- [ ] Unnecessary text formatting steps (Zapier Formatter steps that just pass through)
- [ ] Polling triggers where webhooks exist (biggest task-usage waste)
- [ ] Duplicate data paths (same data written to two places without a clear reason)
- [ ] Missing error handlers — no alert when a scenario fails at 2am
- [ ] Hardcoded IDs or email addresses that will break when accounts change
- [ ] No filter early in the workflow — processing records that should be skipped at step 1

### Audit Notes Template

Keep running notes in a scratch doc as you go:

```
Workflow: [name]
Trigger: [type — polling/webhook/scheduled]
Steps: [count]
Errors (30d): [yes/no — frequency]
Issues found:
  - [issue 1] — severity: high/med/low
  - [issue 2]
Recommended fix: [1-line description]
Est. time to fix: [X min]
Task savings/month: [if applicable]
```

---

## 3. Deliverable

### Loom Video (screen record, ~10–20 min)

Structure:
1. **Intro (1 min):** "Here's what I audited and what I found overall"
2. **Walk each flagged workflow (5–15 min):** Show the live scenario/zap, point at the issue on screen, explain the fix in plain language
3. **Quick wins summary (1–2 min):** "If you only do 3 things, do these"
4. **Cost savings callout (if applicable):** "Switching these 2 polling triggers to webhooks will save you ~X tasks/month, which on your plan saves ~$X"

**Tips:**
- Use Loom's drawing tool to highlight problem areas
- Speak to the client as if they're watching over your shoulder — conversational, no jargon
- Keep it tight. 10 min is better than 25 min.

### Written Report (Markdown, 1–2 pages)

Send as a `.md` file or paste into a Notion page / email body. Structure:

```markdown
# Automation Audit Report — [Client Name]
**Date:** YYYY-MM-DD  
**Workflows audited:** [count]  
**Platform:** Zapier / Make

---

## Summary
[2–3 sentence overall assessment]

## Issues Found

### High Priority
| Workflow | Issue | Fix | Est. Time |
|----------|-------|-----|-----------|
| [name] | [description] | [recommended action] | [X min] |

### Medium Priority
[same format]

### Low Priority / Nice to Have
[same format]

## Estimated Savings
- Task usage reduction: ~X tasks/month
- Cost savings: ~$X/month (based on [plan name])

## Quick Wins (do these first)
1. [Action]
2. [Action]
3. [Action]

---
*Questions about implementing these fixes? Email within 30 days.*
```

### Delivery Method

Email to client with:
- Subject: `Your Automation Audit is Ready`
- Body: 2-3 sentence summary of the biggest finding
- Attachments: Loom link + report (inline or attached .md)

---

## 4. Follow-Up (30-Day Window)

- Client can email with questions about implementing any fix
- Respond within 24 hours (business days)
- Scope: clarifying questions and implementation help for the specific issues found
- Out of scope: building new automations, fixing unrelated workflows, ongoing support
- Upsell opportunity: if client has ongoing needs → offer $99/mo monthly check-in retainer

---

## 5. Edge Cases

**"I can't give you account access"**
→ Ask for a screen recording. Walk through the same checklist visually. Works fine for most audits.

**No actionable findings**
→ Full refund. Email: "I reviewed your workflows and they're actually in solid shape — here's a brief summary of what I checked. Refunding your $199."

**Client wants changes made, not just advice**
→ That's a separate engagement. Quote $150/hr for implementation or a fixed project rate.

**Make vs Zapier differences**
- Make: Scenarios have modules. Look for Router branches that are never triggered.
- Make: Data stores used as pseudo-databases — check if they're growing unbounded.
- Zapier: Paths feature — check all branches have proper filters.
- Zapier: Multi-step zaps on free plan are often hacked together — consolidate on paid.
