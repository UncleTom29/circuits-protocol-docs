# Deployment Guide

Circuits Protocol's production infrastructure relies on a hybrid deployment model: **EC2 for stateful backend processes (via PM2) and Cloudflare Workers for the Next.js frontend.**

There is currently no CI/CD pipeline. Deployments are executed manually via `rsync` and the `wrangler` CLI.

## Architecture Spli

- **Cloudflare Workers (`circuitsprotocol-web`)**: Serves the Next.js frontend (pages, assets) for `circuitsprotocol.com` and `app.circuitsprotocol.com`.
- **EC2 Box**: Runs the actual API routes (`/api/*`), the background indexers, and the job schedulers using `pm2`.

## 1. Preparing the Backend (EC2)

The EC2 instance stores code at `/home/ubuntu/clawdhq`.
**Important**: This directory is NOT a git repository. Code is deployed purely by syncing specific changed files.

### Syncing Changes

Do not rsync the entire directory wholesale. Use `git status --short` to see what changed, and sync only relevant files to prevent deploying unreviewed, in-progress code.

```bash
rsync -av -e "ssh -i /path/to/key.pem"
  <local-path> ubuntu@<ec2-host>:<remote-path>
```

### Dependency Installation

If you added a new dependency (meaning `package.json` or `pnpm-lock.yaml` changed), install them on the box:

```bash
ssh -i /path/to/key.pem ubuntu@<ec2-host>
  "cd /home/ubuntu/clawdhq && export \$(grep -m1 '^GITHUB_PACKAGES_TOKEN=' .env) && pnpm install"
```

### Database Migrations

If Prisma schemas changed, run the migrations against the respective database:

```bash
ssh -i /path/to/key.pem ubuntu@<ec2-host>
  "cd /home/ubuntu/clawdhq && export \$(grep -m1 '^MARKETPLACE_DATABASE_URL=' .env) &&
   cd packages/marketplace-db && pnpm exec prisma migrate deploy && pnpm exec prisma generate"
```

### Rebuilding Packages

Packages must be rebuilt in dependency order:

1. Leaves: `circle`, `clawmem`, `degen-db`, `marketplace-db`, `social-db`
2. `sdk` (depends on `clawmem`)
3. `custody-core`
4. `hosted-agent-runtime`
5. Apps: `apps/indexer`, `apps/web`

Example:
```bash
ssh ... "cd /home/ubuntu/clawdhq/apps/indexer && pnpm run build"
ssh ... "cd /home/ubuntu/clawdhq/apps/web && pnpm run build"
```

### Restarting PM2 Processes

| PM2 Process Name | Target |
|------------------|--------|
| `web` | `apps/web` (Next.js API routes) |
| `indexer-main` | Chain listeners (`apps/indexer/dist/main.js`) |
| `indexer-scheduler` | Subscriptions/orchestration pipeline jobs |
| `indexer-hosted-runtime-scheduler`| Hosted runtime proactive actions |
| `indexer-buyback-scheduler` | Launchpad buybacks |
| `indexer-sportystake-reconciliation`| Degen trading settlement |

Restart only the affected processes:
```bash
ssh ... "pm2 restart indexer-main web && sleep 3 && pm2 list"
```
Verify the restart count (`↺`) doesn't climb rapidly to ensure no crash loops.

## 2. Deploying the Frontend (Cloudflare)

The frontend is deployed to Cloudflare Workers from your local machine.

```bash
cd apps/web
# Harmless placeholder required for the build step
export MARKETPLACE_DATABASE_URL="postgresql://user@localhost:5432/clawdhq_marketplace"
pnpm run build:cf
pnpm exec wrangler deploy
```

Once complete, `wrangler` will push the updated frontend, which automatically proxies `/api/*` requests to the EC2 backend via the `API_PROXY_TARGET` environment variable.
