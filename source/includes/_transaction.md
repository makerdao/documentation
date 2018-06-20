# Transactions

### Basic usage

```javascript
const cdp = await maker.openCdp();
```

Each function in our API that creates a transaction on the blockchain returns a
promise which resolves when the transaction is mined.

### Advanced usage

```javascript
const cdpPromise = maker.openCdp();

// the transaction is being sent to the blockchain;
// if not already pending, it will be pending soon

cdpPromise.onPending(() => console.log('pending!'));
cdpPromise.onMined(() => console.log('mined!'));
cdpPromise.onFinalized(() => console.log('finalized!'));

const cdp = await cdpPromise;

// now the transaction is mined
// and the onMined callback has been called

// if you are using the onFinalized callback, you have to
// call this method at some point.
await cdpPromise.confirm(5);
// 5 = the number of blocks to wait; the default is 3

// now there are five new blocks after the transaction's block
// and the onFinalized callback has been called
```

The promises also have additional methods which can be used to trigger
callbacks when the transaction is pending, or after a certain number of new
blocks have been added after the block containing the transaction (when the
transaction is "finalized").
