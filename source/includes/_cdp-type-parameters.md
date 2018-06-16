# ETH CDP Service

```javascript
const ethCdp = maker.service('cdp');
```
Retrieve the ETH CDP Service through Maker.service('cdp').

The ETH CDP Service exposes the risk parameter information for the Ether CDP type (in single-collateral Dai, this is the only CDP Type)

## **getLiquidationRatio**

```javascript
const ratio = await ethCdp.getLiquidationRatio();
```

* **Params:** none
* **Returns:** promise (resolves to liquidation ratio)

`getLiquidationPenalty()` returns a decimal representation of the liquidation penalty, e.g. 1.5

## **getLiquidationPenalty**

```javascript
const penalty = await ethCdp.getLiquidationPenalty();
```

* **Params:** none
* **Returns:** promise (resolves to liquidation penalty)

`getLiquidationPenalty()` returns a decimal representation of the liquidation penalty, e.g. 0.13

## **getAnnualGovernanceFee**

```javascript
const fee = await ethCdp.getAnnualGovernanceFee();
```

* **Params:** none
* **Returns:** promise (resolves to yearly governance fee)

`getAnnualGovernanceFee()` returns a decimal representation of the liquidation penalty, e.g. 0.005