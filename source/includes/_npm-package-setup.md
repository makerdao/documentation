# Installation

```javascript
import Maker from '@makerdao/makerdao-exchange-integration';
// or:
const Maker = require('@makerdao/makerdao-exchange-integration');
```
Install the package with npm:

`npm install @makerdao/makerdao-exchange-integration`

Once it's installed, import the module into your project.

### UMD

```html
<script src="./maker-exchange-integration.js" />

<script>
var maker = Maker.create('kovan', { privateKey: YOUR_PRIVATE_KEY });

maker.openCdp()
  .then(cdp => cdp.getInfo())
  .then(info => console.log(info));
</script>
```

This library is also accessible as a [UMD module](https://github.com/umdjs/umd).
