# Package Setup

## NPM 

```javascript
import {
  Maker,
  ConfigFactory
} from '@makerdao/makerdao-exchange-integration';

// OR

const {
  Maker,
  ConfigFactory
} = require('@makerdao/makerdao-exchange-integration')
```

The easiest way to install this package is with npm:

`$ npm install @makerdao/makerdao-exchange-integration`

Alternatively, this can be done using yarn:

`$ yarn add @makerdao/makerdao-exchange-integration`

Once installed, import the necessary modules into your project using import or require.

## UMD

```html
<script src="./maker-exchange-integration.js" />

<script> 
var config = ConfigFactory.create('decentralized-oasis-without-proxies');
var maker = new Maker(config);
		
maker.openCdp()
  .then(cdp => cdp.getInfo())
  .then(info => console.log(info));	
</script>
```

This library is also accessible via a [UMD module](https://github.com/umdjs/umd).