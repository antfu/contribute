# Contribution Guide

> This is a general contribution guide for most of [my projects](https://antfu.me/projects).

## Prerequirements

- [Node.js](https://nodejs.org/), using the [latest LTS](https://nodejs.org/en/about/releases/)
- [`pnpm`](https://pnpm.io/) for package mangement, as a replacement of [`npm`](https://docs.npmjs.com/cli/v8)

## Developement Setup

I use [`pnpm`](https://pnpm.io/) for most of the projects, and maybe a few with [`yarn`](https://classic.yarnpkg.com/), I highly recommand you install [`ni`](https://github.com/antfu/ni) so you don't need to worry about the package manager when switching across different projects.

I will use `ni`'s commands in the following code snippets. If you are not using it, you can do convention yourself: `ni = pnpm install`, `nr = pnpm run`

1. [Enable Corepack](#corepack)
3. Install dependencies with `ni` under the project root

### Common Scripts

#### `nr dev`

Start developement environment.

If it's a Node.js package, it will start the build process in watch mode, or [stub the passive watcher when using `unbuild`](https://antfu.me/posts/publish-esm-and-cjs#stubbing).

If it's a frontend project, it commonly starts the dev server that you can developement and see the changes in realtime.

#### `nr play`

If it's a Node.js package, it might start a dev server for the playground. The code is commonly under `playgound/`.

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

<table><tr><td width="400px" valign="top">

#### What's Corepack
  
[Corepack](https://nodejs.org/api/corepack.html) make sure you are using the correct version for package manager when you run corresponding commands. Projects might have `packageManager` field in their `package.json`.

When Corepack is enabled, it will install `v7.1.5` of `pnpm` if you don't have it already and use it do run your command. This make sure everyone working on this project will have exact same behaviour for the dependencies and the lockfile.

</td><td width="600px"><br>

`package.json`

```jsonc
{
  "packageManager": "pnpm@7.1.5"
}
```

</td></tr></table>

### ESLint

I use [ESLint](https://eslint.org/) for both linting and formatting with [my custom config preset](https://github.com/antfu/eslint-config).

<table><tr><td width="400px" valign="top">
  
#### IDE Setup

I recommand using [VS Code](https://code.visualstudio.com/) along with the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).
  
With the settings on the right, you can have auto fix and formatting when you save the code you are editing.

</td><td width="600px"><br>

VS Code's `settings.json`

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true
  }
}
```
  
</td></tr></table>
  

### Why no Prettier

// TODO:
