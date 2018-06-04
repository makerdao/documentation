# Getting Started

### Config Factory

```javascript
// create a config from the 'kovan' preset

const config = ConfigFactory.create('kovan');
```

When instantiating a `Maker` object, you must pass in a config. To make this easy, we have created a `ConfigFactory` which provides you with a few presets cofigs.

The current presets are as follows:

* `'koavn'`
  * Connects you to the Kovan Testnet using Infura
  * Signs transactions using an internal private key
* `'decentralized-oasis-without-proxies'`
  * Connects you to a local testnet (eg Ganache) running at `http://127.1:2000`
  * Signs transactions using testnet-managed keys

*Proxies are contracts that will let you perform multiple actions with a single transaction (eg `open` -> `lock` -> `draw`). This is a safer way to perform sequential actions and will be supported by this library.*


### Instantiation

```javascript
  const maker = new Maker(config);

  const cdp = await maker.openCdp();
```

Gain access to the top-level API by creating a connected instance of the Maker class. 

`new Maker(config)`

Use that class to open a cdp and create a cdp object.

`maker.openCdp()`

*Note: refer to the `Service` section further down for details on service config*

## Example


```javascript
import { 
  Maker, 
  ConfigFactory 
} from '@makerdao/makerdao-exchange-integration';

const config = ConfigFactory.create('decentralized-oasis-without-proxies');
const maker = new Maker(config);

async openLockDraw() {
  cdp = await maker.openCdp();

  await cdp.lockEth('0.25');
  await cdp.drawDai('50');


  const info = await cdp.getInfo();
  console.log(info);
}

openLockDraw();
}
```

Using the `maker` and `cdp` APIs, the program shown on the right opens a cdp, locks 0.25 ETH into it, draws out 50 Dai, and then logs information about our newly opened position to the console.


