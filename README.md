# Frontend Monorepo Boilerplate TypeScript / Tailwind / Material UI

[![CI][ci-badge]][ci-url]
[![TypeScript][typescript-badge]][typescript-url]
[![semantic-release][semantic-badge]][semantic-url]

**Deployments** - Prod / Stage / Storybook

[![CI][deploy-app-prod-badge]][deploy-app-prod-url]
[![CI][deploy-app-stage-badge]][deploy-app-stage-url]
[![CI][deploy-app-storybook-badge]][deploy-app-storybook-url]

[![CI][deploy-website-prod-badge]][deploy-website-prod-url]
[![CI][deploy-website-stage-badge]][deploy-website-stage-url]
[![CI][deploy-website-storybook-badge]][deploy-website-storybook-url]

[![CI][deploy-ui-prod-badge]][deploy-ui-prod-url]
[![CI][deploy-ui-stage-badge]][deploy-ui-stage-url]

Frontend monorepo with focus on best practices and painless developer experience:

- Monorepo setup that can be easily extended 🔧
- Spin it up with single command 🌀
- TypeScript 100% codebase
- Blazing fast builds, lints, tests with Turborepo [remote caching](https://turborepo.org/docs/core-concepts/remote-caching) ⚡

## Requirements

- [Node v20+](https://nodejs.org/)

## Running

_Easily set up a local development environment_

- `npm i`
- `npm run build`
- `npm run dev` - Start all apps 🚀

Visit one of the monorepo apps [localhost:3100](http://localhost:3100/)

## Features:

- [Turborepo v1](https://turborepo.org/) remote cache build system, with fast execution of commands (build, lint, test etc.) on your local machine and CI
- [TypeScript v5](https://github.com/microsoft/TypeScript) codebase with [typescript-eslint](https://github.com/typescript-eslint/typescript-eslint) [`strict-type-checked`](https://typescript-eslint.io/linting/configs/#strict-type-checked) and
  [`stylistic-type-checked`](https://typescript-eslint.io/linting/configs/#stylistic-type-checked) configurations enabled.
- [Vite](https://vitejs.dev/) and [Next.js v14](https://github.com/vercel/next.js) apps
- Monorepo implements 3 styling solutions with shared theme across all apps (pick your use case and remove others).  
  Easily import UI components package into apps:
  - [Vanilla CSS package](https://github.com/mkosir/frontend-monorepo-boilerplate/tree/main/packages/ui)
  - [Tailwind](https://github.com/mkosir/frontend-monorepo-boilerplate/tree/main/packages/ui-tailwind) components library built with [Tailwind v3](https://tailwindcss.com/)
  - [Material UI](https://github.com/mkosir/frontend-monorepo-boilerplate/tree/main/packages/ui-mui) components library built with [MUI v5](https://mui.com/)
- Unit and integration tests with [Jest](https://github.com/facebook/jest) and [React Testing Library](https://github.com/testing-library/react-testing-library). Run any single test in monorepo app/package [instantly](https://github.com/mkosir/typescript-style-guide/raw/main/misc/vscode-jest-runner.gif).
- Linting with [ESLint](https://eslint.org/)
- [Prettier](https://prettier.io/) code formatter
- Git hooks with [Husky](https://github.com/typicode/husky) and [lint-staged](https://github.com/okonet/lint-staged)
- Commit messages must meet [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) format.  
  After staging changes just run `npm run commit` and get instant feedback on your commit message formatting and be prompted for required fields by [Commitizen](https://github.com/commitizen/cz-cli)

## Commands

Bellow commands will be executed on monorepo level - on all apps and packages where npm script exists.

| Command             | Description                                          |
| ------------------- | ---------------------------------------------------- |
| prepare             | Setup git hooks with Husky (executes on npm install) |
| build               | Build all apps and packages (output `build`, `dist`) |
| dev                 | Start all apps                                       |
| lint                | Lint all apps and packages                           |
| lint-staged-husky   | Run prettier and lint on staged files                |
| tsc                 | Run TypeScript compiler                              |
| test                | Run tests on all apps and packages                   |
| storybook           | Start storybooks on all apps and packages            |
| storybook-build     | Build all storybooks (output `build-storybook`)      |
| format-lint         | Lint formatting with Prettier                        |
| format-fix          | Fix formatting with Prettier                         |
| clean               | Remove installed, generated and cached folders       |
| remove-turbo-cache  | Removes Turborepo local cache                        |
| update-dependencies | Update dependencies to their latest versions         |

## Coding Guidelines

Convention over configuration should be followed as much as possible as described in [TypeScript Style Guide](https://github.com/mkosir/typescript-style-guide).

TLDR:

- Strive for data immutability.
- Embrace const assertions.
- Avoid type assertions.
- Embrace discriminated unions.
- Strive for functions to be pure, stateless and have single responsibility.
- Majority of function arguments should be required (use optional sparingly).
- Strong emphasis to keep naming conventions consistent and readable.
- Use named exports.
- Code is organized and grouped by feature. Collocate code as close as possible to where it's relevant.
- UI components must only show derived state and send events, nothing more (no business logic).
- Test business logic, not implementation details.

## Monorepo

Monorepo features and conventions:

- Monorepo is opinionated in order to achieve best developer experience. It's meant to be used as frontend only monorepo, 100% TypeScript, consistent codebase across whole monorepo with automated tooling in place as ESLint, Prettier, TypeScript, conventional commits etc.
- Workspaces:
  - It comes with two workspaces `apps` and `packages`.
  - All configurations (eslint, jest, tailwind etc.) in `packages` are always prefixed with "config-" and imported into other workspaces directly from source without building (never transpiled).
  - All other `packages` beside configurations are always being built/transpiled to `dist/` folder.
- Merging to `main` branch deploys to `stage` environment, creating new GitHub release deploys to `production`.
- Monorepo doesn't implement any high-level architectures (islands, micro-frontends), but is prepared with that in mind, so it can be easily extended (page composition, adding shared state etc.)
