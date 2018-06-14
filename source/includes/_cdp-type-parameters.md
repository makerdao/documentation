# Ether CDP Service

```javascript
const ethCdp = maker.service('ethereumCdp');
```
Retrieve the Ethereum CDP Service through Maker.service('ethereumCdp').

The EthereumCdp exposes the risk parameter information for the CDP type whose collateral is Ether (in single-collateral Dai, this is the only CDP Type)


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