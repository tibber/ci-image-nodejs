# Tibber CI image for Node.js

> Convenience images for running Node.js Circle CI builds

List of image tags:

| Tag |    Based on     |                              Description                              |
| :-: | :-------------: | :-------------------------------------------------------------------: |
| 24  | cimg/node:24.14 | Node.js 24.14, pnpm (Corepack), **Bun**, Kiota, gettext-base. Supports buildx used by `aws-ecr` orb. |

## pnpm (Corepack) and Bun

Both tools are installed on **`PATH`** for the default **`circleci`** user (CircleCI’s Node image convention).

### pnpm — default package manager

- **How:** **Corepack** is enabled with **`--install-directory ~/bin`** (i.e. **`/home/circleci/bin`** on this image).
- **Why that directory:** Image layers run as **`circleci`**, not root. A plain **`corepack enable`** wants to write shims under **`/usr/local/bin`**, which is root-owned, so enabling Corepack for **`pnpm`**/`yarn` into **`~/bin`** avoids permission errors without relying on `sudo` in that step.
- **What you run:** **`pnpm`** / **`pnpx`** from the pruned monorepo as usual. Version follows Corepack’s resolution (see `packageManager` in your repo).

### Bun — optional TypeScript / tooling runtime

- **How:** Official **[Bun](https://bun.sh)** install with **`BUN_INSTALL=/usr/local/bun`**; the directory is created and **`chown`’d** to **`circleci`** so the runtime can live under a fixed **`/usr/local/...`** path while still being writable by the job user.
- **Why not `~/bin`:** Keeps Bun **separate** from Corepack’s shims in **`~/bin`**, avoids name clashes, and gives one obvious prefix (`/usr/local/bun`) for the binary and caches.
- **What you run:** e.g. **`bun ./scripts/ci-task.ts`** without `tsc` or **`node --experimental-strip-types`**. Pin is **`BUN_VERSION`** in `24/Dockerfile` (Renovate: **`oven-sh/bun`**).

Bun does **not** replace pnpm for installing workspace dependencies unless your pipeline calls **`bun`** explicitly.

# This image is built in Dockerhub
