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

Get the current USD price of ETH.

## getMkrPrice

```javascript
const price = await priceFeed.getMkrPrice();
```

Get the current USD price of the governance token MKR.

## setEthPrice

```javascript
await priceFeed.setEthPrice('475.00');
```

Set the current USD price of ETH. 

This requires the necessary permissions and will only be useful in a testing environment.

## setMkrPrice

```javascript
await priceFeed.setMkrPrice('950.00');
```

Set the current USD price of the governance token MKR. 

This requires the necessary permissions and will only be useful in a testing environment.
