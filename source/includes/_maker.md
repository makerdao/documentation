# Maker

## Presets
```javascript
const makerHttp = new Maker('http', {
  privateKey: YOUR_PRIVATE_KEY,
  url: 'https://sai-service.makerdao.com/node'
});

const makerKovan = new Maker('kovan', {
  privateKey: YOUR_PRIVATE_KEY,
  provider: {
    infuraApiKey: YOUR_INFURA_API_KEY
  }
});

const makerTest = new Maker('test');
```

When instantiating a `Maker` object, you pass in the name of a configuration preset
and an options hash.

Available presets are listed below, with the required options for each shown on the
right.

* `'http'`
  * Use Web3.providers.HttpProvider.
* `'kovan'`
  * Use the Kovan testnet via Infura.
* `'test'`
  * Use a local testnet (e.g. Ganache) running at `http://127.0.0.1:2000`, and
sign transactions using testnet-managed keys.

## Options

```javascript
const maker = new Maker('http', {
  privateKey: YOUR_PRIVATE_KEY, // '0xabc...'
  url: 'https://sai-service.makerdao.com/node',
  provider: {
    type: 'HTTP', // 'INFURA', 'TEST'
    network: 'kovan',
    infuraApiKey: YOUR_INFURA_API_KEY
  },
  web3: {
    statusTimerDelay: 2000,
    usePresetProvider: false
  }
  log: false
});
```

* `privateKey`
  * The private key used to sign transactions. If not provided, the first account available from the Ethereum provider will be used.
* `url`
  * The URL of the node to connect to. Only used when `provider.type` is `"HTTP"`.
  * Default value: `"https://sai-service.makerdao.com/node"`
* `provider.infuraApiKey`
  * Your Infura unique access token (the part after infura.io/ when accessing Infura via https). Only used when `provider.type` is `"INFURA"`.
* `provider.type`
  * `"INFURA"`: connect to an Ethereum node via infura
  * `"TEST"`: connect to a local test blockchain at 'http://127.1:2000'
  * `"HTTP"`: connect to an Ethereum node via any arbitrary url
* `web3.statusTimerDelay`
  * Number in milliseconds that represents how often the blockchain connection and account authentication is checked. This allows the library to move out of an authenticated or connected state when it discovers it no longer has access to unlocked accounts, or can no longer connect to a node.
  * Default value: 5000 (5 seconds)
* `web3.usePresetProvider`
  * If `true`, the value `window.web3` (if there is one) will be used as the Provider, instead of creating a new one. For example, this should be true if the library is used in a browser and it should use MetaMask.
  * Default value: `false`
* `log`
  * Set this to `false` to reduce the verbosity of logging.

## **service**

```javascript
const priceFeedService = maker.service('priceFeed');
```

* **Params:** service (string)
* **Returns:** service object

The service function can be used to access services that were injected into your instance of `maker`. See the service documentation sections below.

## **openCdp**

```javascript
const newCdp = await maker.openCdp();
```

* **Params:** none
* **Returns:** promise (resolves to new CDP object)

`maker.openCdp()` will create a new CDP, and then return the CDP object, which can be used to access other CDP functionality.

By default, the promise will resolve when the transaction is mined.


## **getCdp**

```javascript
const cdp = await maker.getCdp(614);
```

* **Params:** CDP ID (integer)
* **Returns:** promise (resolves to CDP object)

`maker.getCdp(id)` creates a CDP object for an existing CDP. The CDP object can then be used to interact with your CDP.
