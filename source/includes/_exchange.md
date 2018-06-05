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
const sellOrder = exchange.sellDai('100.0', 'WETH', '0.30');
```

Sell a set amount of DAI and receive another token in return.

### Parameters
* `daiAmount` - Amount of DAI to sell.
* `tokenSymbol` - Token to receive in return.
* `minFillAmount` - Minimum amount to receive in return.

## buyDai

```javascript
// Buy 100.00 DAI for 0.30 WETH or less.
const buyOrder = exchange.buyDai('100.0', 'WETH', '0.35');
```

Buy a set amount of DAI and give another token in return.

### Parameters
* `daiAmount` - Amount of DAI to buy.
* `tokenSymbol` - Token to give in return.
* `minFillAmount` - Maximum amount to give in return.
