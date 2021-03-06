# npm-github

- [npm-github](#npm-github)
  * [Creating a package](#creating-a-package)
  * [Publish a new version](#publish-a-new-version)
  * [Consume package](#consume-package)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


**[Github hosted](https://docs.github.com/en/packages)** NPM package. Only a template for writing NPM packages on GitHub and there's no reason to install it more than to show how to consume a privately scoped package.

[![Prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier) [![](https://img.shields.io/badge/hacked%20by-thomashagstrom-blueviolet)](https://https://github.com/thomashagstrom)

Based on this guide and the [official documentation](https://docs.github.com/en/packages):

<a href="https://levelup.gitconnected.com/private-npm-packages-in-github-package-registry-fbfda43acab3"><center><p>
<img src="https://miro.medium.com/max/1400/1*I2TaJstcdXWt02Li2pfIUw.png" alt="drawing" width="400"/>
</p>https://levelup.gitconnected.com/private-npm-packages-in-github-package-registry-fbfda43acab3</center></a>

## Creating a package

1. Init a package using `npx tsdx create mylib` ([TypeScript](https://www.typescriptlang.org/)) or `npm init`. 
2. Set [.npmrc](./.npmrc) to the package scope (owner) `@thomashagstrom:registry=https://npm.pkg.github.com`
3. Add [GitHub actions](https://github.com/thomashagstrom/npm-github/actions/new) workflow using the "Publish node.js package" template or this [npm-publish.yml](./.github/workflows/npm-publish.yml) (excluding npmjs).
4. Tag, set [version](https://docs.npmjs.com/about-semantic-versioning) and push.


## Publish a new version

1. Up [version](https://docs.npmjs.com/about-semantic-versioning) in [`package.json`](./package.json)
2. Tag and push
3. [Draft a new Release](https://github.com/thomashagstrom/npm-github/releases) from that tag
4. GitHub Action builds and publishes


## Consume package
These details are valid if the package is private scoped.

1. Open the lib where u want to consume the private NPM package
2. Create a [personal access token](https://github.com/settings/tokens) with `write:packages` scope
3. Config [`.npmrc`](./.npmrc) to use the token (below)
4. Install the scoped package, e.g. `yarn add https://github.com/thomashagstrom/npm-github`

Example [`npmrc`](./.npmrc) config for consuming `thomashagstrom` org scoped packages:

```
@thomashagstrom:registry=https://npm.pkg.github.com/thomashagstrom
//npm.pkg.github.com/:_authToken=MyTopSecretTokenWithPackageScope
```