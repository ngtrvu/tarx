# Investcore Ops Alerting Guide

## Alert Format

When reporting issues to the ops team, always include:

### 1. Issue Summary
- What's failing
- Frequency/pattern
- Source (file:line)

### 2. Affected Users/Resources
- User IDs with ACP links: `https://acp.stag.vn/investment/users/<user_id>`
- Pod names if relevant

### 3. Root Cause Analysis
- Probable causes from code review
- Code location
- Why the issue persists (if recurring)

### 4. Suggested Fix
- Actionable recommendations
- Whether it needs code change or manual intervention

## Example Alert

```
🚨 *Investcore Cronjob Alert*

*Issue:* Auto Submit Stock Accounts failing repeatedly
*Frequency:* Every 5 minutes
*Source:* `account_job_service.go:153`

*Affected Users:*
1. `<user_id>` (<name>)
   → https://acp.stag.vn/investment/users/<user_id>

*Probable Causes:*
1. eKYC not approved
2. Re-KYC required
3. NHSV API error

*Code Location:* `stag/investcore/src/app/stock_account/service/account_job_service.go`

*Why it repeats:* <explanation>

*Suggested Fix:* <recommendation>

_Analysis by TARX 🤖_
```

## Channels

| Project | Google Chat Webhook | Config |
|---------|---------------------|--------|
| Investcore | ops-channels.json | `investcore.gchat_webhook` |
