# Price Service

```javascript
const price = maker.service('price');
```

Retrieve the PriceService through `Maker.service('price')`.

The PriceService exposes the collateral and governance tokens' price information that is 
reported by the oracles in the Maker system.

## getEthPrice

```javascript
const ethPrice = await price.getEthPrice();
```

Get the current USD price of ETH.

## getMkrPrice

```javascript
const mkrPrice = await price.getMkrPrice();
```

Get the current USD price of the governance token MKR.

## getPethPrice

```javascript
await pethPrice = price.getPethPrice();
```

Get the current USD price of PETH (pooled ethereum) according to the Maker price oracle.

## setEthPrice

```javascript
await price.setEthPrice('475.00');
```

Set the current USD price of ETH. 

This requires the necessary permissions and will only be useful in a testing environment.

## setMkrPrice

```javascript
await price.setMkrPrice('950.00');
```

Set the current USD price of the governance token MKR. 

This requires the necessary permissions and will only be useful in a testing environment.

## getWethToPethRatio

```javascript
await price.getWethToPethRatio();
```

Returns the current W-ETH to PETH ratio.