# Joplin notes and synchronization

Notes application monorepo with desktop, mobile, command-line, and server packages, built primarily with TypeScript.

This repository is a separately imported source snapshot of [joplin](https://github.com/laurent22/joplin). Upstream contributors created the imported application; local work is recorded in the commits after the source import. See [Upstream source](UPSTREAM_SOURCE.md) for attribution.

## Read the history accurately

The local history starts with a source import on November 3, 2026. The parent year directory and the “Original project year” field do not establish a historical contribution date or a release tag. The imported upstream commit and release are not recorded in the available provenance file.

## Navigate the source

| Path | Responsibility |
| --- | --- |
| [packages/app-desktop/](packages/app-desktop/) | Desktop application |
| [packages/app-mobile/](packages/app-mobile/) | Mobile application |
| [packages/app-cli/](packages/app-cli/) | Command-line application |
| [packages/lib/](packages/lib/) | Shared note and synchronization logic |
| [packages/server/](packages/server/) | Synchronization server |

## Prepare development

Read `CLAUDE.md`, `package.json`, `.yarnrc.yml`, and the package you intend to modify. Use the pinned Yarn version and compatible Node.js runtime. The root postinstall runs a build; desktop and mobile packages need their own platform tooling.

The commands below are existing project entry points, to run after their toolchain, dependency, and service prerequisites are ready:

```sh
yarn buildParallel
yarn tsc --noEmit
```

## Validation scope

The documentation change was checked for local link targets, manifest command references, and whitespace errors. Application builds, dependency installation, and service-backed test suites were not run for this documentation change. These instructions do not establish deployment readiness.

## Preserve upstream licensing

Missing upstream license notices were restored from the official repository. [License restoration](LICENSE_RESTORATION.md) records the retrieval revision, exact source URLs, and SHA-256 hashes. That revision does not identify the imported application snapshot. Read per-file and subtree notices as well as the root license before redistribution. This documentation does not change the license of imported code.

## Install and run locally

Use the Node.js and Yarn versions declared in the root manifest. Installation runs the repository postinstall build:

```sh
yarn install --immutable
yarn buildParallel
yarn workspace joplin start
```

The last command launches the command-line workspace in its development environment. Desktop and mobile builds need additional platform tooling. To explore the synchronization server with its development database instead, inspect and run:

```sh
docker compose -f docker-compose.server-dev.yml up --build
```

That Compose configuration exposes the app on port 22300 and PostgreSQL on port 5432; ensure those ports are free and treat its included database credentials as local-only values.

## Plan a deployment

Use `Dockerfile.server`, `docker-compose.server.yml`, and `.env-sample` as server configuration entry points. Set the public base URL, database settings, and persistent storage for the target environment. Client builds are platform-specific deliverables; building the server does not package desktop or mobile clients.
