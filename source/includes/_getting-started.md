# Getting Started

## Installation

```javascript
import Maker from '@makerdao/makerdao-exchange-integration';
// or:
const Maker = require('@makerdao/makerdao-exchange-integration');
```
Install the package with npm:

`npm install @makerdao/makerdao-exchange-integration`

Once it's installed, import the module into your project as shown on the right.

### UMD

```html
<script src="./maker-exchange-integration.js" />

<script>
var maker = new Maker('kovan', { privateKey: YOUR_PRIVATE_KEY });

maker.openCdp()
  .then(cdp => cdp.getInfo())
  .then(info => console.log(info));
</script>
```

This library is also accessible as a [UMD module](https://github.com/umdjs/umd).

## Quick Example

```javascript
import Maker from '@makerdao/makerdao-exchange-integration';

const maker = new Maker("kovan", { privateKey: YOUR_PRIVATE_KEY });

async function openLockDraw() {
  cdp = await maker.openCdp();

  await cdp.lockEth(0.25);
  await cdp.drawDai(50);

  const info = await cdp.getInfo();
  console.log(info);
}

openLockDraw();
```

Using the [Maker](#maker) and [Cdp](#cdp) APIs, the code shown on the right
opens a cdp, locks 0.25 ETH into it, draws out 50 Dai, and then logs information
about the newly opened position to the console.
