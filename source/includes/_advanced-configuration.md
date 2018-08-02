# Advanced Configuration

```javascript
const customMaker = Maker.create('http', {
  log: 'BunyanLogger',
  exchange: 'ZeroExExchangeService',
  web3: [
    'MyCustomWeb3Service',
    {
      speed: 'maximum plaid'
    }
  ],
});
```

You can take advantage of the pluggable architecture of this library by choosing
different implementations for services. An example configuration is shown at
right. (The ability to add your own custom implementations is still in
development.)
