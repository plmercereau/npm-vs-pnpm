##

Both `yarn`, `npm` and `pnpm` support workspaces, but in a slight different way.

Npm's adoption of workspaces is quite new, and we were likely using an `npm` version that were not using them. We now are.

This repo is a basic monorepo set with `pnpm`. What we want to do is to install eveything in the `nhost` directory without taking into account the rest of the repo:

```sh
cd nhost
npm i
```

Output:

```
npm ERR! code EUNSUPPORTEDPROTOCOL
npm ERR! Unsupported URL Type "workspace:": workspace:*

npm ERR! A complete log of this run can be found in:
npm ERR!     ~/.npm/_logs/2022-12-09T17_15_24_731Z-debug-0.log
```

Npm is resolving the parent `package.json`, and tries to install the entire workspace. But in the `unrelated` package, a dependency is using the `pnpm` syntax: `"workspace:*"`.
Therefore it fails.

To solve it:

```sh
cd nhost
npm i --no-workspaces
```
