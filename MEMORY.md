# MEMORY.md - Long-term Memory

## Who I Am
- **Name:** TARX
- **Role:** Systems oversight assistant
- **Owner:** Vu Nguyen (@ngtrvu, GMT+7)
- **Rule:** Ask before making system changes; investigate freely

## Working Ethics (Core Principles)
1. **Do good** — Always act in good faith
2. **Do no harm** — Never harm anyone or anything
3. **Analyze & inform** — Provide useful, data-driven insights
4. **Minimal changes** — Make the smallest change necessary to achieve the goal

## Key Infrastructure

### Authentication
- **SSH Key:** `~/.ssh/tarx_key` (ed25519, no passphrase)
- **GitHub access:** `ngtrvu/marketdb`

### Models (Amazon Bedrock)
- Opus 4.5: `amazon-bedrock/global.anthropic.claude-opus-4-5-20251101-v1:0`
- Sonnet 4: `amazon-bedrock/global.anthropic.claude-sonnet-4-20250514-v1:0`

### Tools
- **Claude Code:** `~/.local/bin/claude` (v2.1.29, Bedrock-enabled)
- Configured as CLI backend and skill in OpenClaw

### Workspaces
- OpenClaw: `/home/admin/.openclaw/workspace`
- Code: `~/code`
- MarketDB: `~/code/marketdb`
- Stag: `~/code/stag`

### GitHub Machine User
- Account: `tarx-tinilab`
- Email: `vu@tinilab.com`
- Profile: https://github.com/tarx-tinilab
- Access to: `ngtrvu/marketdb`, `ngtrvu/stag`, `ngtrvu/nextcms`
- GitHub CLI (`gh`) authenticated with PAT token

## Projects

### NextCMS (`~/code/nextcms`)
- Headless CMS / blogging platform
- **Stack:** Bun monorepo, Turbo, Hono backend, Prisma ORM, PostgreSQL
- **Infra:** GKE (`services-sg-prod`, `asia-southeast1-a`), Artifact Registry
- **GitHub:** `github.com/ngtrvu/nextcms`

**Work completed (2026-02-07/08):**
- ✅ Set up local Postgres test container (port 5433)
- ✅ Fixed test fixtures for VarChar(24) DB constraints
- ✅ Fixed API key middleware (siteId extraction from path)
- ✅ All 43 backend tests passing
- ✅ PR #201: `docs/content-api` — API key management + tests (merged)
- ✅ PR #202: `ci/deploy-backend` — GitHub Actions deploy workflow
  - Auto-deploy on push to main
  - Skaffold + Helm deployment
  - Rollout verification + auto-rollback on failure
  - Requires `GCP_SA_KEY` secret

**Key files:**
- Dockerfile: `apps/backend/Dockerfile`
- Helm chart: `deploy/backend/`
- Skaffold: `deploy/skaffold.yaml`
- Deploy workflow: `.github/workflows/deploy-backend.yml`
- Test workflow: `.github/workflows/test.yml`

### MarketDB (`~/code/marketdb`)
- Market data platform
- Components: backend (Go/Python), crawler, DAGs, jobs, investcore
- GitHub: `github.com/ngtrvu/marketdb`

## Preferences
- Vu concerned about token costs → use Sonnet for daily chat, Opus for heavy tasks
- HEARTBEAT.md kept empty to avoid background API calls

## Session History & Token Usage

### 2026-02-03 - Initial Setup & MarketDB Cleanup
**Session:** 57edfede-44b4-483c-8184-a6a3bc8f29fa
**Model:** Sonnet 4.5 | **Tokens:** 53,244 | **Cost:** ~$0.30-0.52

**Accomplished:**
- ✅ Configured Claude Code CLI with Opus 4.5 as default model
  - Settings: `~/.config/claude-code/settings.json`
  - Alias added to `~/.bashrc`
- ✅ Security audit (SSH keys, permissions, services, firewall review)
- ✅ MarketDB investcore cleanup
  - Removed unused analytics: `payment_analytics_bq.py`, `portfolio_stats_bq.py`
  - Fixed broken CLI commands in `main.py`
  - Created AUM calculation task (`aum_bq.py`) with CLI command
  - PR: `cleanup/remove-unused-analytics` (3 commits)
  - GitHub: `ngtrvu/marketdb`

**Git Config:**
- Name: TARX
- Email: Tarx@vuclaw
