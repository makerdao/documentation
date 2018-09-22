# Transactions

### TransactionObject Lifecycle Hooks

```javascript
const txObject = await cdp.wipeDai(1);

// the transaction is being sent to the blockchain;
// if not already pending, it will be pending soon

txObject.onPending(() => console.log('pending!'));
txObject.onMined(() => console.log('mined!'));
txObject.onFinalized(() => console.log('finalized!'));
txObject.onError(() => console.log('error'));

const pending = txObject.isPending();
const mined = txObject.isPending();
const finalized = txObject.isFinalized();
const error = txObject.isError();

// if you are using the onFinalized callback, you have to
// call this method at some point.
await txObject.confirm(5);
// 5 = the number of blocks to wait; the default is 3

// now there are five new blocks after the transaction's block
// and the onFinalized callback has been called
```

`TransactionObjects` have methods which can be used to trigger
callbacks when the transaction is pending, or after a certain number of new
blocks have been added after the block containing the transaction (when the
transaction is "finalized").

### TransactionObject Transaction Data

```javascript
const txObject = await cdp.drawDai(1);
const hash = txObject.hash();
const fees = txObject.fees();
const timeStamp = txObject.timeStamp();
const timeStampSubmitted = txObject.timeStampSubmitted();
```

`TransactionObjects` also have a few methods to provide details on the transaction:
	* `hash`: transaction hash
	* `fees()`: amount of ether spent on gas
	* `timeStamp()`: timestamp of when transaction was mined
	* `timeStampSubmitted()`: timestamp of when transaction was submitted to the network


### onNewTransaction

```javascript
maker.service('transactionManager').onNewTransaction(tx => {
  tx.onPending(() => {
    console.log(`${tx.metadata.contract}.${tx.metadata.method}: pending`);
  });
});
```

The `onNewTransaction` function in the `transactionManager` service allows you to register a callback that gets called every time a transaction is initiated by the dai.js library.
