# Ladle Contributing Guide

Thanks for your interest to contribute to Ladle. Please take a moment and read through this guide:

## Repository

Ladle is a monorepo using pnpm workspaces. We use Node v16. The package manager used to install and link dependencies must be [pnpm v7](https://pnpm.io/). It can be installed as:

```sh
npm install -g pnpm@7
```

Install the depedencies after forking and cloning the repository

```sh
pnpm install
```

## Developing

The main `@ladle/react` package can be found in `packages/ladle`. You can quickly test and debug your changes in `@ladle/react` by running `packages/example` (it's a toy project so feel free to add more stories there):

```sh
cd packages/example
pnpm ladle serve
pnpm ladle build
```

## Tests

Before creating a PR you should make sure that all tests are still passing:

```sh
# root
pnpm typecheck
pnpm lint

# root or individual packages
pnpm build
pnpm test
```

There are unit tests and also end-to-end tests powered by Playwright in `e2e/` folder. If you are adding a new feature, you will be almost always asked to add a new e2e test. You can add it to one of the existing suites / test applications or create new one.

## Documentation

If applicable, your changes should be also documented on [ladle.dev](https://ladle.dev/). The doc site can be started as:

```sh
cd packages/website
pnpm start
```

## Changesets

Ladle uses [changesets](https://github.com/changesets/changesets) to manage the changelog and releases. If your are changing `@ladle/react` you need to [add a changeset](https://github.com/changesets/changesets/blob/main/docs/adding-a-changeset.md) (or you will be prompted in your PR):

```sh
pnpm changeset
```

You will be asked to select the scope (pick `@ladle/react`) and version (patch, minor, major). Then you should describe it:

- WHAT the change is
- WHY the change was made
- HOW a consumer should update their code (if applicable)

This will create an `.changeset/*.md` file that gets merged with your PR and attached to the release by admins later.

## Creating a new package

You can create a new package in `packages` or `e2e` (playwright apps+tests). It needs to be added to:

- `package.json#workspaces`
- `pnpm-workspace.yaml#packages`
