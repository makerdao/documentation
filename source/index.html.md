---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# MakerDAO Exchange Integration

[![tests][tests]][tests-url]
[![coverage][cover]][cover-url]

# MakerDAO Exchange Integration

[![tests][tests]][tests-url]
[![coverage][cover]][cover-url]

**MakerDAO Exchange Integration** is a JavaScript library that makes it easy to build applications on top of MakerDAO's platform of smart contracts. You can use Maker's contracts to open Collateralized Debt Positions, withdraw loans in Dai, trade tokens on OasisDEX, and more.

The library features a pluggable, service-based architecture, which allows users maximal control when integrating the Maker functionality into existing infrastructures. It also includes convenient configuration presets for out-of-the-box usability, a powerful smart contract state inspector, and support for both front-end and back-end applications.

Maker's entire suite of contracts will eventually be accessible through this library—including the DAO governance and the upcoming multi-collateral release—but functionality is limited in the current alpha version to the following areas:

* Opening and shutting CDPs
* Locking and unlocking collateral
* Withdrawing and repaying Dai
* Automated token conversions
* Token contract functionality for WETH, PETH, MKR, Dai, and ETH
* Buying and selling MKR and Dai with built-in DEX integration

# Source code setup

`git clone https://github.com/makerdao/makerdao-integration-poc`
`npm install`


## Prerequisites

[![node][node]][node-url]
[![npm][npm]][npm-url]
      
- [Node.js](http://es6-features.org)

## Features

- [Webpack](https://webpack.js.org/guides) (v3.5.5)
    - [Webpack Dev Server](https://github.com/webpack/webpack-dev-server) (v2.7.1)
    - [Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement)
    - [Clean Webpack Plugin](https://github.com/johnagan/clean-webpack-plugin) (v0.1.16)
- [ECMAScript 6](http://es6-features.org)
- [Babel](https://babeljs.io/docs/setup/#installation) (v6.26.0)
- [ESLint](https://eslint.org/docs/user-guide/getting-started) (v4.5.0)
- [Jest](https://facebook.github.io/jest/docs/en/getting-started.html) (v20.0.4)
- [Sass](http://sass-lang.com/guide)

## Inspect contract state

Start the dev server using `npm start`, then open [http://localhost:9000](http://localhost:9000)


## Commands

- `npm start` - start the dev server
- `npm run build:backend` - create backend build in `dist` folder
- `npm run build:frontend` - create frontend build in `dist` folder
- `npm run lint` - run an ESLint check
- `npm run coverage` - run code coverage and generate report in the `coverage` folder
- `npm test` - run all tests
- `npm run test:watch` - run all tests in watch mode
- `npm run test:net` - launch a Ganache test chain and deploy MakerDAO's contracts on it

# NPM Package Setup 

`npm install @makerdao/makerdao-exchange-integration`

First, import the necessary modules in your JS code:

`import { Maker, ConfigFactory } from '@makerdao/makerdao-exchange-integration';`

Then create a connected instance of the Maker class and use it to call CDP methods, like you see in the JS snippet in the right panel.

```javascript
async setupFunction() {
  const config = ConfigFactory.create('kovan');

  return await new Maker(config);
}

async someOtherFunction() {
  const maker = await setupFunction();
  const cdp = await maker.openCdp();

  return await cdp.lockEth();
}
```

[npm]: https://img.shields.io/badge/npm-5.3.0-blue.svg
[npm-url]: https://npmjs.com/

[node]: https://img.shields.io/node/v/webpack-es6-boilerplate.svg
[node-url]: https://nodejs.org

[tests]: http://img.shields.io/travis/jluccisano/webpack-es6-boilerplate.svg
[tests-url]: https://travis-ci.org/jluccisano/webpack-es6-boilerplate

[cover]: https://codecov.io/gh/jluccisano/webpack-es6-boilerplate/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/jluccisano/webpack-es6-boilerplate
