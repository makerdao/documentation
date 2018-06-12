# Getting Started

### Config Factory

When instantiating a `Maker` object, you must pass in a configuration preset.

The current presets are as follows:

* `'kovan'`
  * Connects you to the Kovan Testnet using Infura
  * Signs transactions using a private key that you provide
* `'decentralized-oasis-without-proxies'`
  * Connects you to a local testnet (eg Ganache) running at `http://127.1:2000`
  * Signs transactions using testnet-managed keys

*Note: refer to the `Custom Config Files` section further down for details on customizing the config file*

*Side Note: Proxies are contracts that will let you perform multiple actions with a single transaction (eg `open` -> `lock` -> `draw`). This is a safer way to perform sequential actions and will be supported by this library.*


### Instantiation

```javascript
const maker = new Maker("kovan", { privateKey: process.env.KOVAN_PRIVATE_KEY });

  const cdp = await maker.openCdp();
```

Gain access to the top-level API by creating a connected instance of the Maker class. 

`new Maker(config)`

Use that class to open a cdp and create a cdp object.

`maker.openCdp()`


## Example


```javascript
import { Maker } from '@makerdao/makerdao-exchange-integration';

const maker = new Maker("kovan", { privateKey: process.env.KOVAN_PRIVATE_KEY });

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


