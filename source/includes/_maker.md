# Maker

## Presets
```javascript
const makerBrowser = Maker.create('browser');

const makerHttp = Maker.create('http', {
  privateKey: YOUR_PRIVATE_KEY,
  url: 'http://some-ethereum-rpc-node.net'
});

const makerKovan = Maker.create('kovan', {
  privateKey: YOUR_PRIVATE_KEY,
  provider: {
    infuraApiKey: YOUR_INFURA_API_KEY
  }
});

const makerTest = Maker.create('test');
```

When instantiating a `Maker` object, you pass in the name of a configuration preset
and an options hash.

Available presets are listed below, with the required options for each shown on the
right.

* `'browser'`
  * Use the provider from the browser (e.g. MetaMask).
* `'http'`
  * Use Web3.providers.HttpProvider.
* `'kovan'`
  * Use the Kovan testnet via Infura.
* `'test'`
  * Use a local testnet (e.g. Ganache) running at `http://127.0.0.1:2000`, and
sign transactions using testnet-managed keys.
* `'mainnet'`
  * Use the main Ethereum network via Infura.

## Options

```javascript
const maker = Maker.create('http', {
  privateKey: YOUR_PRIVATE_KEY, // '0xabc...'
  url: 'http://some-ethereum-rpc-node.net',
  provider: {
    type: 'HTTP', // 'INFURA', 'TEST'
    network: 'kovan',
    infuraApiKey: YOUR_INFURA_API_KEY
  },
  web3: {
    statusTimerDelay: 2000,
    transactionSettings: {
      gasPrice: 12000000000
    }
  },
  log: false,
  confirmedBlockCount: 8
});
```

* `privateKey`
  * The private key used to sign transactions. If not provided, the first account available from the Ethereum provider will be used.
* `url`
  * The URL of the node to connect to. Only used when `provider.type` is `"HTTP"`.
* `provider.infuraApiKey`
  * Your Infura unique access token (the part after infura.io/ when accessing Infura via https). Only used when `provider.type` is `"INFURA"`.
* `provider.type`
  * `"INFURA"`: connect to an Ethereum node via infura
  * `"TEST"`: connect to a local test blockchain at 'http://127.1:2000'
  * `"HTTP"`: connect to an Ethereum node via any arbitrary url
* `web3.statusTimerDelay`
  * Number in milliseconds that represents how often the blockchain connection and account authentication is checked. This allows the library to move out of an authenticated or connected state when it discovers it no longer has access to unlocked accounts, or can no longer connect to a node.
  * Default value: 5000 (5 seconds)
* `web3.transactionSettings`
  * Object containing transaction options to be applied to all transactions sent through the library.
  * Default value: `{ gasLimit: 4000000 }`
* `log`
  * Set this to `false` to reduce the verbosity of logging.
* `confirmedBlockCount`
  * Number of blocks to wait after a transaction has been mined when calling `confirm`. See [transactions](#transactions) for further explanation. Default is 5.

## **authenticate**

```javascript
await maker.authenticate();
```

After creating your Maker instance, and before using any other methods, run this. It makes sure all services are initialized, connected to any remote API's, and properly authenticated.

## **service**

```javascript
const priceService = maker.service('price');
```

* **Params:** service (string)
* **Returns:** service object

The service function can be used to access services that were injected into your instance of `maker`. See the service documentation sections below.

## **openCdp**

```javascript
const newCdp = await maker.openCdp();
```

* **Params:** none
* **Returns:** promise (resolves to new CDP object once mined)

`maker.openCdp()` will create a new CDP, and then return the CDP object, which can be used to access other CDP functionality.

The promise will resolve when the transaction is mined.


## **getCdp**

```javascript
const cdp = await maker.getCdp(614);
```

* **Params:** CDP ID (integer)
* **Returns:** promise (resolves to CDP object)

`maker.getCdp(id)` creates a CDP object for an existing CDP. The CDP object can then be used to interact with your CDP.

## Units

```javascript
import Maker from '@makerdao/dai';
const {
  MKR,
  DAI,
  ETH,
  WETH,
  PETH,
  USD_ETH,
  USD_MKR,
  USD_DAI
} = Maker;

// These are all identical:

// each method has a default type
cdp.lockEth(0.25);
cdp.lockEth('0.25');

// you can pass in a currency unit instance
cdp.lockEth(ETH(0.25));
cdp.lockEth(ETH.wei(250000000000000000));

// you can pass the unit as an options argument
cdp.lockEth(0.25, { unit: ETH });
cdp.lockEth(250000000000000000, { unit: ETH.wei });

const eth = ETH(5);
eth.toString() == '5.00 ETH';

const price = USD_ETH(500);
price.toString() == '500.00 USD/ETH';

// multiplication handles units
const usd = eth.times(price);
usd.toString() == '2500.00 USD';

// division does too
const eth2 = usd.div(eth);
eth2.isEqual(eth);
```

Methods that take numerical values as input can also take instances of token
classes that the library provides. These are useful for managing precision,
keeping track of units, and passing in wei values.

Most methods that return numerical values return them wrapped in one of these
classes.

There are two types:

* **currency units**, which represent an amount of a type of currency
* **price units**, which represent an exchange rate between two currencies.

The classes that begin with `USD` are price units; e.g. `USD_ETH` represents
the price of ETH in USD.

Useful instance methods:

* **toNumber**: return the raw JavaScript value. This may fail for very large numbers.
* **toBigNumber**: return the raw value as a [BigNumber](https://github.com/MikeMcl/bignumber.js).
* **isEqual**: compare the values and symbols of two different instances.
* **toString**: show the value in human-readable form, e.g. "500 USD/ETH".
