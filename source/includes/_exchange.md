# Exchange Service

```javascript
const exchange = maker.service('exchange');
```

Retrieve the OasisExchangeService (or alternative implementation) 
through `Maker.service('exchange')`.

The exchange service allows to buy and sell DAI, MKR, and other tokens. The default 
OasisExchangeService implementation uses the OasisDEX OTC market for this.

## sellDai

```javascript
// Sell 100.00 DAI for 0.30 WETH or more.
const sellOrder = await exchange.sellDai('100.0', 'WETH', '0.30');
```

Sell a set amount of DAI and receive another token in return.

* **Parameters**
	* `daiAmount` - Amount of DAI to sell.
	* `tokenSymbol` - Token to receive in return.
	* `minFillAmount` - Minimum amount to receive in return.
* **Returns:** promise (resolves to OasisOrder once mined)

## buyDai

```javascript
// Buy 100.00 DAI for 0.30 WETH or less.
const buyOrder = await exchange.buyDai('100.0', 'WETH', '0.35');
```

Buy a set amount of DAI and give another token in return.

* **Parameters**
	* `daiAmount` - Amount of DAI to buy.
	* `tokenSymbol` - Token to give in return.
	* `minFillAmount` - Maximum amount to give in return.
* **Returns:** promise (resolves to OasisOrder once mined)

## OasisOrder

```javascript
const buyOrder = await exchange.buyDai('100.0', 'WETH', '0.35');
const fillAmount = buyOrder.fillAmount();
const gasPaid = buyOrder.fees();
const created = buyOrder.created();
```

`OasisOrders` have a few methods:
	* `fillAmount`: amount of token received in exchange
	* `fees()`: amount of ether spent on gas
	* `created()`: timestamp of when transaction was mined