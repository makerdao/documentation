---
title: Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - getting-started
  - maker
  - cdp
  - price
  - cdp-type-parameters
  - exchange
  - system-status
  - events
  - advanced-configuration
  - source-code-setup

search: true
---

# MakerJS

[![tests][tests]][tests-url]
[![coverage][cover]][cover-url]

**MakerJS** is a JavaScript library that makes it easy to build applications on top of MakerDAO's platform of smart contracts. You can use Maker's contracts to open Collateralized Debt Positions (CDPs), withdraw loans in Dai, trade tokens on OasisDEX, and more.

The library features a pluggable, service-based architecture, which allows users maximal control when integrating the Maker functionality into existing infrastructures. It also includes convenient configuration presets for out-of-the-box usability, a powerful smart contract state inspector, and support for both front-end and back-end applications.

Maker's entire suite of contracts will eventually be accessible through this library—including the DAO governance and the upcoming multi-collateral release—but functionality is limited in the current alpha version to the following areas:

* Opening and closing CDPs
* Locking and unlocking collateral
* Withdrawing and repaying Dai
* Automated token conversions
* Token contract functionality for WETH, PETH, MKR, Dai, and ETH
* Buying and selling MKR and Dai with built-in DEX integration

[tests]: http://img.shields.io/travis/jluccisano/webpack-es6-boilerplate.svg
[tests-url]: https://travis-ci.org/jluccisano/webpack-es6-boilerplate
[cover]: https://codecov.io/gh/jluccisano/webpack-es6-boilerplate/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/jluccisano/webpack-es6-boilerplate
