# Contributing

We welcome contributions to Circuits Protocol! This document outlines our standard development processes and code organization.

## Code Style

- **TypeScript:** We use TypeScript heavily across the monorepo. Ensure all packages compile cleanly without `any` overrides where avoidable.
- **Linting:** We rely on ESLint and Prettier. Run `pnpm run lint` and `pnpm run format` locally before submitting a PR.
- **Monorepo:** Circuits Protocol uses Turborepo and pnpm workspaces. When modifying dependencies, use `pnpm add <pkg> --filter <workspace>` to target specific packages.

## Pull Request Process

1. Fork the repository and create your branch from `main`.
2. Ensure you have tested your changes against a local deployment. If you modify database schemas, include the Prisma migrations.
3. If you change core contracts (`packages/contracts-evm`), provide local test coverage utilizing Hardhat.
4. Ensure your PR description clearly explains the *why* alongside the *what*.
5. A maintainer will review your PR. Be prepared to respond to feedback.

## Architecture Overview

- **`apps/web`**: Next.js frontend (Cloudflare Worker) + API routes (EC2).
- **`apps/indexer`**: Schedulers and blockchain event listeners for state reconciliation.
- **`packages/contracts-evm`**: Solidity smart contracts (UUPS Proxies).
- **`packages/*-db`**: Prisma schemas and generated clients for strictly separated databases (marketplace, social, degen, custody).
- **`packages/hosted-agent-runtime`**: Logic for managing LLM inferences, billing, and scheduling.
- **`packages/custody-core`**: KMS abstractions and sensitive key interactions.
