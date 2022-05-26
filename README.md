# Contribution Guide

Hi! We are really excited that you are interested in contributing. This is a general contribution guide for most of [my projects](https://antfu.me/projects). Before submitting your contribution, please make sure to take a moment and read through the following guide:

## 📦 Prerequirements

- [Node.js](https://nodejs.org/), using the [latest LTS](https://nodejs.org/en/about/releases/)
- [`pnpm`](https://pnpm.io/) for package management, as a replacement of [`npm`](https://docs.npmjs.com/cli/v8)

## 👨‍💻 Repo Setup

We use [`pnpm`](https://pnpm.io/) for most of the projects, and maybe a few with [`yarn`](https://classic.yarnpkg.com/), we highly recommend you install [`ni`](https://github.com/antfu/ni) so you don't need to worry about the package manager when switching across different projects.

We will use `ni`'s commands in the following code snippets. If you are not using it, you can do convention yourself: `ni = pnpm install`, `nr = pnpm run`

1. [Enable Corepack](#corepack)
2. Install dependencies with `ni` under the project root

## 💡 Common Scripts

### `nr dev`

Start development environment.

If it's a Node.js package, it will start the build process in watch mode, or [stub the passive watcher when using `unbuild`](https://antfu.me/posts/publish-esm-and-cjs#stubbing).

If it's a frontend project, it commonly starts the dev server that you can development and see the changes in realtime.

### `nr play`

If it's a Node.js package, it might start a dev server for the playground. The code is commonly under `playground/`.

### `nr build`

Build the project for production.

### `nr lint`

We use [ESLint](https://eslint.org/) for **both linting and formatting**. It also lint for JSON, YAML and Markdown files if exists.

You can run `nr lint --fix` to have ESLint do the auto formatting and linting fix for you.

Learn more about the [ESLint Setup](#eslint).

[**We don't use Prettier**](#no-prettier).

### `nr test`

Run the tests. We mostly using [Vitest](https://vitest.dev/) - a replacement of [Jest](https://jestjs.io/).

You can filter the tests to be run by `nr test [match]`, for example, `nr test foo` will only run test files that contains `foo`.

Config options are often under the `test` felid of `vitest.config.ts` or `vite.config.ts`.

Vitest runs in [watch mode by default](https://vitest.dev/guide/features.html#watch-mode), so you can modify the code and see the test result automatically, which is great for [Test-driven development](https://en.wikipedia.org/wiki/Test-driven_development). To run the test only once, you can do `nr test --run`.

For some projects, we might have multiple types of tests set up. For example `nr test:unit` for unit tests, `nr test:e2e` for end-to-end tests. `nr test` commonly run them together, you can run them separately as needed.

### `nr docs`

If the project contains a documentation, you can run `nr docs` to start the documentation dev server. Use `nr docs:build` to build the docs for production.

### `nr`

For more, you can run bare `nr`, which will prompt a list of all available scripts.

## 🙌 Sending Pull Request

### Discuss First

Before you start to work on a feature pull request, it's always better to open an feature request issue first to discuss with the maintainers whether the feature is desired and the design of those features. This would help save time for both the maintainers and the contributors and help features to be shipped faster.

For typo fixes, it's recommend to batch multiple typo fixes into one pull request to maintain a cleaner commit history.

### Commit Convention

We use [Conventional Commits](https://www.conventionalcommits.org/) for commits, which allow the changelog to be auto generated based on the commits. Please read it through the guide.

Note that `fix:` and `feat:` are for **actually code changes** (that might affects logics).
For typo or document changes, use `docs:` or `chore:` instead:

- ~~`fix: typo`~~ -> `docs: fix typo`

### Pull Request

If you don't know how to send a Pull Request, we recommend reading [the guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

When send a pull request, make sure your PR title also follows the [Commit Convention](#commit-conventions).

If you PR fixes or resolves an existing issue, please add a line as following in your PR description (replace `123` will real issue number):

```markdown
fix #123
```

This will allow GitHub to know they are linked and automatically close the issue when the PR get merged. Learn more at [the guide](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword).

It's Ok to have multiple commits in a single PR, you don't need to rebase or force push for your changes as we will use `Squash and Merge` to squash the commits into one on merging.

## 📖 References

### Corepack

#### TL;DR

To enable it, run

```bash
corepack enable
```

You only need to do it once after Node.js is installed.

<table><tr><td width="500px" valign="top">

#### What's Corepack

[Corepack](https://nodejs.org/api/corepack.html) makes sure you are using the correct version for package manager when you run corresponding commands. Projects might have `packageManager` field in their `package.json`.

When Corepack is enabled, under projects with configures on the right, it will install `v7.1.5` of `pnpm` if you don't have it already and use that version to run your command. This make sure everyone working on this project will have exact same behavior for the dependencies and the lockfile.

</td><td width="500px"><br>

`package.json`

```jsonc
{
  "packageManager": "pnpm@7.1.5"
}
```

</td></tr></table>

### ESLint

We use [ESLint](https://eslint.org/) for both linting and formatting with [`@antfu/eslint-config`](https://github.com/antfu/eslint-config).

<table><tr><td width="500px" valign="top">

#### IDE Setup

We recommend using [VS Code](https://code.visualstudio.com/) along with the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).

With the settings on the right, you can have auto fix and formatting when you save the code you are editing.

</td><td width="500px"><br>

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

### No Prettier

Since ESLint is already configured to format the code, there is no need to duplicate the functionality of Prettier. To format the code, you can run `nr lint --fix` or referring the [ESLint section](#eslint) for IDE Setup.

If you have Prettier installed in your editor, we recommend you to disable it when working on the project to avoid conflicting.
