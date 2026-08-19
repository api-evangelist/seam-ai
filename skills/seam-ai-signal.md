---
name: Signal
description: Use when building account-based marketing campaigns, automating prospecting workflows, configuring account scoring and intent tracking, setting up multi-channel plays, or managing sales routing and contact enrichment. Agents should reach for this skill when working with ABM strategy, account intelligence, automated outreach orchestration, or sales process automation.
metadata:
    mintlify-proj: signal
    version: "1.0"
---

# Seam AI Skill Reference

## Product Summary

Seam AI is an AI-native account-based marketing (ABM) platform that automates the entire workflow from identifying best-fit accounts to executing multi-channel campaigns. It combines account scoring (Fit, Intent, Signals), intelligent contact prospecting, data enrichment, and automated plays (workflows) to turn account intelligence into pipeline. Agents use Seam to configure ICP fit criteria, monitor buying signals, build dynamic audiences, create automated plays, and route contacts to sales reps. Key files and concepts: Fit Score (ICP matching), Intent (engagement tracking), Signals (external triggers), Personas (buying committee targeting), Plays (automated workflows), Routing (contact assignment), Audiences (dynamic segments). Primary docs: https://docs.getseam.ai

## When to Use

Reach for this skill when:
- **Configuring account intelligence:** Setting up Fit Score criteria, defining personas, creating audiences, or monitoring intent signals
- **Building automated workflows:** Creating plays that prospect contacts, enrich data, and deploy to CRM/sales engagement platforms
- **Managing data connections:** Integrating Salesforce, HubSpot, SalesLoft, Outreach, LinkedIn Ads, Marketo, or other systems
- **Setting up routing rules:** Configuring how contacts are assigned to sales reps (account owner, round robin, territory, custom fields)
- **Optimizing ABM campaigns:** Analyzing play performance, adjusting audience criteria, managing credit consumption
- **Troubleshooting prospecting issues:** Debugging why contacts aren't being found, enriched, or routed correctly
- **Implementing tiered account strategies:** Creating different plays and audiences for A/B/C-tier accounts with varying automation levels

## Quick Reference

### Core Concepts

| Concept | Purpose | When to Use |
|---------|---------|------------|
| **Fit Score** | AI-powered ICP matching (A/B/C/D grades) | Filter all plays; always include as base criterion |
| **Intent** | Engagement tracking (website, email, ads, Bombora) | Identify accounts actively researching; trigger time-sensitive plays |
| **Signals** | External events (new hires, funding, job posts) | Create urgency; trigger buying committee prospecting |
| **Personas** | Target roles/titles (VP Sales, CMO, Director RevOps) | Define who to prospect; set contact limits per account |
| **Audiences** | Dynamic segments combining fit/intent/signals | Trigger plays; sync to ad platforms; route to sales |
| **Plays** | Automated workflows (trigger → prospect → enrich → deploy) | Execute campaigns; prospect contacts; route to sequences |
| **Routing** | Contact assignment rules (account owner, round robin, territory) | Ensure contacts reach correct rep; prevent orphan leads |

### Configuration Workflow

1. **Connect data sources** (Settings → Connections): Salesforce, HubSpot, SalesLoft, Outreach, LinkedIn Ads, Marketo, Bombora
2. **Define Fit Score criteria** (Fit Score → Add fit): 5-10 custom criteria based on closed-won patterns; backtest on 45 accounts
3. **Create personas** (Personas): 3-5 core personas with titles, seniority, keywords, exclusions; set contact limits
4. **Configure signals** (Signals): New hires, funding, job openings, social mentions; prioritize by conversion
5. **Build audiences** (Audiences): Combine fit + intent + signals + account attributes; test with 50-100 accounts first
6. **Set up routing queues** (Routing): Define rep groups (round robin, regional, vertical, account-based)
7. **Create plays** (Plays): Define trigger → audience filter → personas → enrichment → routing → deployment

### Credit Consumption

Credits are consumed by:
- **Prospecting:** Finding contacts matching personas (per contact found)
- **Enrichment:** Validating emails, phone numbers, multi-provider waterfall (per contact)
- **Fit scoring:** AI research and evaluation (per account scored)

Monitoring: Track credit burn rate in play analytics; adjust contact limits or audience size if needed.

## Decision Guidance

### When to Use X vs Y

| Decision | Use X When | Use Y When |
|----------|-----------|-----------|
| **Always-On vs One-Off Play** | Continuous automation (website visitors, new hires) | Single-run campaigns (event follow-up, list processing) |
| **Account Owner vs Round Robin Routing** | Accounts already assigned; maintain consistency | New inbound leads; fair distribution across team |
| **A/B/C Tier Automation** | A-tier: manual + plays; B-tier: automated plays; C-tier: nurture only | All accounts same treatment (rare; usually tiered) |
| **Fit Score Backtest Pass** | Proceed to production scoring | Refine criteria and retest (don't skip validation) |
| **Contact Limit Setting** | A-tier: 5-7 contacts; B-tier: 3-4; C-tier: 1-2 | Higher limits = better coverage but higher costs |
| **Audience Size** | 50-100 accounts for testing; 1000+ for scaling | Under 20 accounts (too small); over 10,000 (lacks specificity) |
| **Bombora Intent vs First-Party** | Offsite research tracking; weekly updates | Website visits, email engagement; real-time updates |

## Workflow

### Typical Task: Launch Your First Play

1. **Understand the use case:** What accounts do you want to target? When should they be engaged? Which contacts matter?
2. **Check existing configuration:** Verify Fit Score is calibrated, personas are defined, routing queues exist
3. **Build the audience:** Combine fit (A/B minimum), intent (optional), signals (optional), exclusions (competitors, customers, late-stage opps)
4. **Test with small set:** Run play on 20-50 accounts first; verify routing works, sequences load, messaging resonates
5. **Configure the play:** Set trigger (always-on or one-off), audience filter, personas to prospect, contact limits, enrichment, routing, deployment channels
6. **Monitor performance:** Track accounts processed, contacts found, enrichment quality, response rates, pipeline attribution
7. **Optimize:** Adjust audience criteria, contact limits, or personas based on results; pause underperformers

### Typical Task: Configure Fit Score

1. **Analyze closed-won customers:** What do your best customers have in common? (size, industry, tech stack, business model)
2. **Define 5-10 criteria:** Use natural language questions (e.g., "Does this company have 500-2000 employees?" "Do they use Snowflake?")
3. **Include disqualification criteria:** Competitors, wrong industries, too small/large
4. **Backtest on 45 accounts:** 15 good fits, 15 bad fits, 15 random; verify A/B scores match good customers
5. **Refine if needed:** Adjust criteria if results don't align; retest
6. **Deploy to production:** Score your full TAM; use in all plays as base filter

### Typical Task: Set Up Routing

1. **Define routing method:** Account owner (existing accounts), round robin (new leads), territory (geographic), custom field (complex rules)
2. **Create routing queues:** Group reps by method (e.g., "SDR Round Robin", "Enterprise AEs - West", "Healthcare Specialists")
3. **Set fallback rules:** Primary method → fallback → default (ensure no orphan contacts)
4. **Test with small play:** Verify contacts appear with correct owners in CRM and sales engagement tools
5. **Document routing logic:** Explain why leads route where they do for team reference

## Common Gotchas

- **Skipping Fit Score backtest:** Don't deploy without validating on 45 accounts; poor criteria waste credits and damage brand
- **Forgetting to exclude competitors/customers:** Automating outreach to wrong accounts burns credits and hurts reputation
- **Setting contact limits too high:** More contacts = better coverage but exponential credit costs; start with 3 per account
- **Routing AFTER deployment:** Route before deploying to sales engagement tools, not after; wrong email sender will send
- **Audience too large or too small:** Under 20 accounts = not worth automating; over 10,000 = lacks specificity; target 50-1000
- **Not testing plays before scaling:** Always run on small audience first; verify routing, sequences, and messaging work
- **Ignoring credit consumption:** Monitor burn rate; adjust contact limits or audience size if consuming too fast
- **Personas too broad:** "Marketing" catches product marketing, content, brand, etc.; use exclusions to narrow
- **Intent signals without fit filter:** Don't chase every website visitor; always filter by Fit Score first
- **Orphan contacts from failed routing:** Always set fallback routing rules; don't let contacts drop through cracks
- **Stale Fit Score criteria:** Retest quarterly; company changes (funding, hiring, acquisitions) can shift fit
- **Deploying to wrong CRM field:** Verify custom field mappings before running plays; wrong fields break workflows

## Verification Checklist

Before launching a play or campaign:

- [ ] **Data connections verified:** All systems (CRM, sales engagement, ad platforms) syncing correctly
- [ ] **Fit Score calibrated:** Backtest passed; A/B scores match good customers; criteria documented
- [ ] **Personas defined:** 3-5 core personas with titles, seniority, keywords, exclusions; contact limits set
- [ ] **Audience criteria clear:** Fit filter included; intent/signals/exclusions defined; audience size 50-1000 accounts
- [ ] **Routing configured:** Method chosen (account owner/round robin/territory); queues created; fallback rules set
- [ ] **Play tested:** Run on 20-50 accounts; verify contacts found, enriched, routed correctly, deployed to right systems
- [ ] **Messaging aligned:** Sequences, email templates, ad copy match audience and trigger
- [ ] **Credit budget confirmed:** Estimated consumption calculated; within annual bucket
- [ ] **Stakeholder buy-in:** Sales, marketing, ops teams aligned on personas, routing, automation
- [ ] **Monitoring plan:** Know which metrics to track (accounts processed, contacts found, response rates, pipeline)

## Resources

**Comprehensive navigation:** https://docs.getseam.ai/llms.txt — Full page-by-page listing of all documentation

**Critical pages:**
1. [Plays Guide](https://docs.getseam.ai/guides/actions/plays) — Understand play workflow, types, examples, best practices
2. [Fit Score Guide](https://docs.getseam.ai/guides/monitoring-and-intelligence/fit-score) — Configure ICP criteria, backtest, grading system
3. [Onboarding Checklist](https://docs.getseam.ai/onboarding/getting-started/checklist) — Step-by-step setup (2-3 weeks): data sources, ICP, personas, audiences, first play

**Support:** support@getseam.ai

---

> For additional documentation and navigation, see: https://docs.getseam.ai/llms.txt