# ts-monorepo

## Setup

- Code lives in projects under `frontend/`.
- Projects can depend on each other via imports starting with `:` (ex: `import foo from ':proj-01/foo';`). This is configured via TS path mapping.
- We are in the process of migrating to project references (once they are deeply cycle-free). So, projects can either have project references enabled (extend `tsconfig.dts.json`) or disabled (extend `tsconfig.base.json`).
- This repo's configuration is representative, but it is on a much smaller scale. Internally, we have ~70k TS files across ~900 projects.
- There is a mix of TS and JS files.

## Build

- Only for projects with project references enabled.
- `yarn tsc -b frontend/typescript/tsconfig.build.json` builds to `.tsbuild`
- Cached in CI for subsequent incremental builds. Timestamps for edited files are updated prior to build in order to signal changes to TS compiler.
- We run `tsc -b` in parallel for better performance on cache misses.
