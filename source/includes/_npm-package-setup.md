# NPM package setup 

`npm install @makerdao/makerdao-exchange-integration`

First, import the necessary modules in your JS code:

`import { Maker, ConfigFactory } from '@makerdao/makerdao-exchange-integration';`

Then create a connected instance of the Maker class and use it to call CDP methods, like you see in the JS snippet in the right panel.

```javascript
async setupFunction() {
  const config = ConfigFactory.create('kovan');

  return await new Maker(config);
}

async someOtherFunction() {
  const maker = await setupFunction();
  const cdp = await maker.openCdp();

  return await cdp.lockEth();
}
```
