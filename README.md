# Tibber CI image for Node.js

> Convenience images for running Node.js Circle CI builds

List of image tags:

| Tag |    Based on     |                              Description                              |
| :-: | :-------------: | :-------------------------------------------------------------------: |
| 24  | cimg/node:24.14 | Node.js 24.14, pnpm (Corepack), **Bun**, Kiota, gettext-base. Supports buildx used by `aws-ecr` orb. |

## Bun

**[Bun](https://bun.sh)** is installed for **optional** use in CircleCI (and local Docker runs): run **TypeScript** helpers without `tsc` or `node --experimental-strip-types`, e.g. `bun ./scripts/ci-task.ts`.

- **Install path:** `/usr/local/bun` — `bun` is on **`PATH`** for the default user.
- **Version:** pinned in `24/Dockerfile` as **`BUN_VERSION`** (Renovate: `oven-sh/bun`). Check the Dockerfile for the current release.

The default package manager for Tibber Node monorepos remains **pnpm** (Corepack); Bun does not replace pnpm unless your pipeline explicitly invokes it.

# This image is built in Dockerhub
