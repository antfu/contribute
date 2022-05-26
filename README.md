# Contribution Guide

> This is a general contribution guide for most of [my projects](https://antfu.me/projects).

## Prerequirements

- [Node.js](https://nodejs.org/), using the [latest LTS](https://nodejs.org/en/about/releases/)
- [`pnpm`](https://pnpm.io/) for package mangement, as a replacement of [`npm`](https://docs.npmjs.com/cli/v8)

## Developement Setup

I use [`pnpm`](https://pnpm.io/) for most of the projects, and maybe a few with [`yarn`](https://classic.yarnpkg.com/), I highly recommand you install [`ni`](https://github.com/antfu/ni) so you don't need to worry about the package manager when switching across different projects.

> I will use `ni`'s commands in the following code snippets. If you are not using it, the convention is `ni = pnpm install`, `nr = pnpm run`

1. [Enable Corepack](#corepack)
3. Install dependencies with `ni` under the project root

### Common Scripts

#### `nr dev`

Start developement environment.

If it's a Node.js package, it will start the build process in watch mode, or [stub the passive watcher when using `unbuild`](https://antfu.me/posts/publish-esm-and-cjs#stubbing).

If it's a frontend project, it commonly starts the dev server that you can developement and see the changes in realtime.

#### `nr build`

Build the project for production.

#### `nr lint`

I use [ESLint](https://eslint.org/) for both linting and formatting. It also lint for JSON, YAML and Markdown files if exists.

You can run `nr lint --fix` to have ESLint do the auto formatting and linting fix for you.

Learn more about the [ESLint Setup](#eslint).

[**I don't use Prettier**](#why-no-prettier).

#### `nr test`

Run the tests. I mostly using [Vitest](https://vitest.dev/) - a replacement of [Jest](https://jestjs.io/).

You can filter the tests to be run by `nr test [match]`, for example, `nr test foo` will only run test files that contains `foo`.

Config options are often under the `test` feild of `vitest.config.ts` or `vite.config.ts`.

Vitest runs in watch mode by default, so you can modifiy the code and see the test result automatically, which is great for [Test-driven development](https://en.wikipedia.org/wiki/Test-driven_development). To run the test only once, you can do `nr test --run`.

## References

### Corepack

#### TL;DR

To enable it, run

```bash
corepack enable
```

You only need to do it once after Node.js is installed.

#### What's Corepack

[Corepack](https://nodejs.org/api/corepack.html) make sure you are using the correct version for package manager when you run corresponding commands. Projects might have `packageManager` field in their `package.json`, for example:

```json
{
  "packageManager": "pnpm@7.1.5"
}
```

When Corepack is enabled, it will install `v7.1.5` of `pnpm` if you don't have it already and use it do run your command. This make sure everyone working on this project will have exact same behaviour for the dependencies and the lockfile.

### ESLint

// TODO:

### Why no Prettier

// TODO:
