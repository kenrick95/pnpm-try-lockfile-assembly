# Lockfile assembly issue

Ref: https://github.com/pnpm/pnpm/pull/4475

Note: `git-branch-lockfile` is the config, not `use-git-branch-lockfile` :sweat_smile:

Imagine this scenario:

1. `master` branch has `pkg-a` that depends on react 17 & react-dom 17
2. on `feature-1` branch, developer upgrades `pkg-a`'s dependencies: react 18 & react-dom 18
   this creates `pnpm-lock.feature-1.yaml`
3. `feature-1` is merged to `master` branch
4. on `master` branch, run `pnpm install --merge-git-branch-lockfiles`

## Repro

1. Clone this repo
2. Run `pnpm install --merge-git-branch-lockfiles`


## Expected

- `pnpm-lock.feature-1.yaml` is deleted
- `pnpm-lock.yaml` is updated

## Actual

- `pnpm-lock.feature-1.yaml` is deleted
- `pnpm-lock.yaml` is **not** updated


## Environment

- Node 14.19.3 (npm 6.14.17)
- pnpm 7.9.0
- MacOS 11.6.7
