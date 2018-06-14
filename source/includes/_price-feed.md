# Price Feed Service

```javascript
const priceFeed = maker.service('priceFeed');
```

Retrieve the PriceFeedService through `Maker.service('priceFeed')`.

The PriceFeedService exposes the collateral and governance tokens price information that is 
reported by the oracles in the Maker system.

## getEthPrice

```javascript
const price = await priceFeed.getEthPrice();
```

* **Params:** none
* **Returns:** promise (resolves to ether price)

Get the current USD price of ETH.

## getPethPrice

```javascript
const price = await priceFeed.getPethPrice();
```

* **Params:** none
* **Returns:** promise (resolves to peth price)

Get the current USD price of PETH.

## getMkrPrice

```javascript
const price = await priceFeed.getMkrPrice();
```

* **Params:** none
* **Returns:** promise (resolves to mkr price)

Get the current USD price of the governance token MKR.

## getWethToPethRatio

```javascript
const ethToPeth = await priceFeed.getWethToPethRatio();
```

* **Params:** none
* **Returns:** promise (resolves to weth to peth ratio)

Get the price of PETH in ETH, e.g. 1.01 means 1 PETH is worth 1.01 ETH

## setEthPrice

```javascript
await priceFeed.setEthPrice('475.00');
```

* **Params:** none
* **Returns:** TODO

Set the current USD price of ETH. 

This requires the necessary permissions and will only be useful in a testing environment.

## setMkrPrice

```javascript
await priceFeed.setMkrPrice('950.00');
```

* **Params:** none
* **Returns:** TODO

Set the current USD price of the governance token MKR. 

This requires the necessary permissions and will only be useful in a testing environment.


