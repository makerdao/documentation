# CDP

Now that you've used `maker` to either open a new CDP or retrieve an existing one, you can use the returned `cdp` object to call functions on it.

## **Properties**

### `.id`

This is the ID of the CDP object. You can pass this ID to
[`Maker.getCdp`](#getcdp).

## **getDebtValue**

```javascript
const daiDebt = await cdp.getDebtValue();
const usdDebt = await cdp.getDebtValue(Maker.USD);
```

* **Params:** [currency unit](#units) (optional)
* **Returns:** promise (resolves to the amount of outstanding debt)

  `cdp.getDebtValue()` returns the amount of debt that has been borrowed against the collateral in the CDP. By default it returns the amount of Dai as a [currency unit](#units), but can return the equivalent in USD if the first argument is `Maker.USD`.

## **getGovernanceFee**

```javascript
const mkrFee = await cdp.getGovernanceFee();
const usdFee = await cdp.getGovernanceFee(Maker.USD);
```

* **Params:** [currency unit](#units) (optional)
* **Returns:** promise (resolves to the value of the accrued governance fee in USD)

`cdp.getGovernanceFee()` returns the value of the accrued governance fee. By default it returns the amount of MKR as a [currency unit](#units), but can return the equivalent in USD if the first argument is `Maker.USD`.

## **getCollateralizationRatio**

```javascript
const ratio = await cdp.getCollateralizationRatio();
```

* **Params:** none
* **Returns:** promise (resolves to the collateralization ratio)

`cdp.getCollateralizationRatio()` returns the USD value of the collateral in the CDP divided by the USD value of the Dai debt for the CDP, e.g. `2.5`.

## **getLiquidationPrice**

```javascript
const ratio = await cdp.getLiquidationPrice();
```

* **Params:** none
* **Returns:** promise (resolves to the liquidation price)

`cdp.getLiquidationPrice()` returns the price of Ether in USD that causes the CDP to become unsafe (able to be liquidated), all other factors constant. It returns a `USD_ETH` [price unit](#units).

## **getCollateralValue**

```javascript
const ethCollateral = await cdp.getCollateralValue();
const pethCollateral = await cdp.getCollateralValue(Maker.PETH);
const usdCollateral = await cdp.getCollateralValue(Maker.USD);
```

* **Params:** [currency unit](#units) (optional)
* **Returns:** promise (resolves to collateral amount)

`cdp.getCollateralValue()` returns the value of the collateral in the CDP. By default it returns the amount of ETH as a [currency unit](#units), but can return the equivalent in PETH or USD depending on the first argument.

## **isSafe**

```javascript
const ratio = await cdp.isSafe();
```

* **Params:** none
* **Returns:** promise (resolves to boolean)

`cdp.isSafe()` returns true if the cdp is safe, that is, if the USD value of its collateral is greater than or equal to USD value of the its debt multiplied by the liquidation ratio.

## **enoughMkrToWipe**

```javascript
const enoughMkrToWipe = await cdp.enoughMkrToWipe(10000000000000000000, DAI.wei);
```

* **Params:** amount of Dai to wipe
* **Returns:** promise (resolves to boolean)

`cdp.enoughMkrToWipe(dai)` returns true if the current account owns enough MKR to wipe the specified amount of Dai from the CDP.

## **lockEth**

```javascript
return await cdp.lockEth(10000000000000000000, ETH.wei);
// or equivalently
return await cdp.lockEth(100, ETH);
```

* **Params:** amount to lock in the CDP, in units defined by the price service.
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.lockEth(eth)` abstracts the token conversions needed to lock collateral in a CDP. It first converts the ETH to WETH, then converts the WETH to PETH, then locks the PETH in the CDP.

## **drawDai**

```javascript
return await cdp.drawDai(10000000000000000000, DAI.wei);
// or equivalently
return await cdp.drawDai(100, DAI);
```

* **Params:** amount to draw (in Dai, as string)
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.drawDai(dai)` withdraws the specified amount of Dai as a loan against the collateral in the CDP. As such, it will fail if the CDP doesn't have enough PETH locked in it to remain at least 150% collateralized.

## **wipeDai**

```javascript
return await cdp.wipeDai(10000000000000000000, DAI.wei);
// or equivalently
return await cdp.wipeDai(100, DAI);
```

* **Params:** amount to repay (in Dai, as string)
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.wipeDai(dai)` sends Dai back to the CDP in order to repay some (or all) of its outstanding debt.

*Note: CDPs accumulate MKR governance debt over their lifetime. This must be paid when wiping dai debt, and thus MKR must be acquired before calling this method.*

## **freePeth**

```javascript
return await cdp.freePeth(100, PETH);
// or equivalently
return await cdp.freePeth(10000000000000000000, PETH.wei);
```

* **Params:** amount of Peth collateral to free from the CDP, in units defined by the price service.
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.freePeth(peth)` withdraws the specified amount of PETH and returns it to the owner's address. As such, the contract will only allow you to free PETH that's locked in excess of 150% of the CDP's outstanding debt.

## **give**

```javascript
return await cdp.give('0x046ce6b8ecb159645d3a605051ee37ba93b6efcc');
```

* **Params:** Ethereum address (string)
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.give(address)` transfers ownership of the CDP from the current owner to the address you provide as an argument.

## **shut**

```javascript
return await cdp.shut();
```

* **Params:** none
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.shut()` wipes all remaining dai, frees all remaining collateral, and deletes the CDP. This will fail if the caller does not have enough DAI and MKR to wipe all debt.

## **bite**

```javascript
return await cdp.bite();
```

* **Params:** none
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`cdp.bite()` will initiate the liquidation process of an undercollateralized CDP
