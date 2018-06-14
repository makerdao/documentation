# System Status

```javascript
const ethCdp = maker.service('ethereumCdp');
```
To access system status information, retrieve the Ethereum CDP Service through Maker.service('ethereumCdp').

## **getSystemCollateralization**

```javascript
const systemRatio = await ethCdp.getSystemCollateralization();
```

* **Params:** none
* **Returns:** promise (resolves to system collateralization ratio)

`getSystemCollateralization()` returns the collateralization ratio for the entire system, e.g. 2.75

## **getTargetPrice**

```javascript
const targetPrice = await ethCdp.getTargetPrice();
```

* **Params:** none
* **Returns:** promise (resolves to target price)

`getTargetPrice()` returns the target price of Dai in USD, that is, the value to which Dai is soft-pegged, e.g. 1.0