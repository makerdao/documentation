# Getting Started

## Installation

```javascript
import Maker from '@makerdao/dai';
// or:
const Maker = require('@makerdao/dai');
```
Install the package with npm:

`npm install @makerdao/dai`

Once it's installed, import the module into your project as shown on the right.

### UMD

```html
<script src="./dai.js" />

<script>
Maker.create('http',{
	privateKey: YOUR_PRIVATE_KEY,
	url: 'https://kovan.infura.io/v3/YOUR_INFURA_PROJECT_ID'
})
	.then(maker => { window.maker = maker })
	.then(() => maker.authenticate())
  .then(() => maker.openCdp())
  .then(cdp => console.log(cdp.id));
</script>
```

This library is also accessible as a [UMD module](https://github.com/umdjs/umd).

## Quick Example

```javascript
import Maker from '@makerdao/dai';

async function openLockDraw() {
	const maker = await Maker.create("http", {
		privateKey: YOUR_PRIVATE_KEY,
		url: 'https://kovan.infura.io/v3/YOUR_INFURA_PROJECT_ID'
	});

  await maker.authenticate();
  const cdp = await maker.openCdp();

  await cdp.lockEth(0.25);
  await cdp.drawDai(50);

  const debt = await cdp.getDebtValue();
  console.log(debt.toString); // '50.00 DAI'
}

openLockDraw();
```

Using the [Maker](#maker) and [Cdp](#cdp) APIs, the code shown on the right
opens a cdp, locks 0.25 ETH into it, draws out 50 Dai, and then logs information
about the newly opened position to the console.
