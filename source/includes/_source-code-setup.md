# Source code setup

1. `git clone https://github.com/makerdao/makerdao-integration-poc`
2. `npm install`


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

## Run the tests

The test suite is configured to run on a Ganache test chain. Before running the tests (`npm test`), the test chain will start, and the script will deploy all the Maker contracts to the chain.

To avoid waiting for this process every time you run the tests, use the command `npm run test:watch`.

If you want to deploy the contracts to a test chain independently from the test suite, use `npm run test:net`.

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


[npm]: https://img.shields.io/badge/npm-5.3.0-blue.svg
[npm-url]: https://npmjs.com/

[node]: https://img.shields.io/node/v/webpack-es6-boilerplate.svg
[node-url]: https://nodejs.org
