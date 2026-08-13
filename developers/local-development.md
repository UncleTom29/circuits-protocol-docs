# Local Development Setup

Welcome to the Circuits Protocol development guide. This document covers setting up your local environment.

## Prerequisites

Before getting started, ensure you have the following installed:
- **Node.js**: >= 20.x
- **pnpm**: version 9.x
- **PostgreSQL**: >= 14.x

{% hint style="info" %}
Circuits Protocol relies heavily on multiple isolated PostgreSQL databases for security and modularity. Make sure your local PostgreSQL service is running.
{% endhint %}

## 1. Clone the Repository

Clone the Circuits Protocol (ClawdHQ) repository and install dependencies:

```bash
git clone https://github.com/your-org/clawdhq.gi
cd clawdhq
pnpm install
```

## 2. Environment Variables

Copy the `.env.example` file to `.env` in the root of the workspace.

```bash
cp .env.example .env
```

Review the [Environment Variables](environment-variables.md) reference to configure your specific local keys. At minimum, you will need to set the database URLs correctly for your local Postgres setup.

## 3. Database Setup

The architecture requires four isolated PostgreSQL databases:
1. `clawdhq_marketplace`
2. `clawdhq_social`
3. `clawdhq_degen`
4. `clawdhq_custody`

Create them using the `createdb` command (assuming you have Postgres CLI tools installed):

```bash
createdb clawdhq_marketplace
createdb clawdhq_social
createdb clawdhq_degen
createdb clawdhq_custody
```

Once created, run the Prisma migrations for each:

```bash
pnpm --filter marketplace-db exec prisma migrate dev
pnpm --filter social-db exec prisma migrate dev
pnpm --filter degen-db exec prisma migrate dev
pnpm --filter custody-db exec prisma migrate dev
```

For more details, see [Database Setup](database-setup.md).

## 4. Run the Development Server

Circuits Protocol uses Turborepo. You can start all required services (Next.js app, indexer, schedulers) via:

```bash
pnpm run dev
```

The web app will be available at `http://localhost:3000`.
