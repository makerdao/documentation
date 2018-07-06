# CDP

Now that you've used `maker` to either open a new CDP or retrieve an existing one, you can use the returned `cdp` object to call functions on it.

## **getId**

```javascript
const id = await cdp.getId();
```

* **Params:** none
* **Returns:** promise (resolves to CDP ID)

Use `cdp.getId()` to retrieve the ID from a CDP object. You may need to use the ID as a parameter for other functions.


## **getInfo**

```javascript
const info = await cdp.getInfo();
const lockedPeth = info.ink;
```

* **Params:** none
* **Returns:** promise (resolves to CDP info object)

`cdp.getInfo()` will return a few distinct properties of the CDP:

* lad: The Ethereum address associated with the owner of the CDP
* ink: Amount of PETH collateral locked in the CDP (this returns the same value as `cdp.getCollateralValueInPeth()`)
* art: Outstanding "normalized" debt - tax only (this is not the actual debt.  Use one of the getDebtValue functions for that)
* ire: Outstanding "normalized" debt (this is not the actual total amount owed.  Use one of the getDebtValue and getMkrFee functions for that)

Please refer to the [MakerDAO White Paper](https://makerdao.com/whitepaper/DaiDec17WP.pdf) or reach out on our [community chat](https://chat.makerdao.com/home) if you need help understanding how these variables are used in the system.

## **getDebtValueInDai**

```javascript
const daiDebt = await cdp.getDebtValueInDai();
```

* **Params:** none
* **Returns:** promise (resolves to the amount of outstanding debt in Dai)

`cdp.getDebtValueDai()` returns the amount of Dai that has been borrowed against the collateral in the CDP.

## **getDebtValueInUSD**

```javascript
const debtInUSD = await cdp.getDebtValueInUSD();
```

* **Params:** none
* **Returns:** promise (resolves to the amount of outstanding debt in USD)

`cdp.getDebtValueInUSD()` returns the value of the borrowed Dai in USD terms.  This will return the same value as `cdp.getDebtValueInDai` as long as the Target Price is 1.

## **getMkrFeeInUSD**

```javascript
const feeInUSD = await cdp.getMkrFeeInUSD();
```

* **Params:** none
* **Returns:** promise (resolves to the value of the accrued governance fee in USD)

`cdp.getMkrFeeInUSD()` returns the USD value of the accrued governance fee.

## **getMkrFeeInMkr**

```javascript
const feeInMkr = await cdp.getMkrFeeInMkr();
```

* **Params:** none
* **Returns:** promise (resolves to the value of the accrued governance fee in MKR)

`cdp.getMkrFeeInMkr()` returns the amount of MKR token needed to pay off the accrued governance fee

## **getCollateralizationRatio**

```javascript
const ratio = await cdp.getCollateralizationRatio();
```

* **Params:** none
* **Returns:** promise (resolves to the collateralization ratio)

`cdp.getCollateralizationRatio()` returns the USD value of the collateral in the CDP divided by the USD value of the Dai debt for the CDP, e.g. 2.5

## **getLiquidationPriceEthUSD**

```javascript
const ratio = await cdp.getLiquidationPriceEthUSD();
```

* **Params:** none
* **Returns:** promise (resolves to the liquidation price)

`cdp.getLiquidationPriceEthUSD()` returns the price of Ether in USD that causes the CDP to become unsafe (able to be liquidated), all other factors constant.

## **getCollateralValueInUSD**

```javascript
const collateral = await cdp.getCollateralValueInUSD();
```

* **Params:** none
* **Returns:** promise (resolves to collateral amount)

`cdp.getCollateralValueInUSD()` returns value of the collateral in the CDP in terms of USD

## **getCollateralValueInEth**

```javascript
const collateral = await cdp.getCollateralValueInEth();
```

* **Params:** none
* **Returns:** promise (resolves to collateral amount)

`cdp.getCollateralValueInEth()` returns the value of the collateral in the CDP in terms of Ether

## **getCollateralValueInPeth**

```javascript
const collateral = await cdp.getCollateralValueInPeth();
```

* **Params:** none
* **Returns:** promise (resolves to collateral amount)

`cdp.getCollateralValueInPeth()` returns the value of the collateral in the CDP in terms of Peth

## **isSafe**

```javascript
const ratio = await cdp.isSafe();
```

* **Params:** none
* **Returns:** promise (resolves to boolean)

`cdp.isSafe()` returns true if the cdp is safe, that is if the USD value of the collateral in the CDP is greater than or equal to USD value of the debt in the CDP multiplied by the liquidation ratio.

## **lockEth**

```javascript
return await cdp.lockEth(10000000000000000000, ETH.wei);
// or equivalently
return await cdp.lockEth(100, ETH);
```

* **Params:** amount to lock in the CDP, in units defined by the price service.
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.lockEth(eth)` abstracts the token conversions needed to lock collateral in a CDP. It first converts the ETH to WETH, then converts the WETH to PETH, then locks the PETH in the CDP.


## **drawDai**

```javascript
return await cdp.drawDai(10000000000000000000, DAI.wei);
// or equivalently
return await cdp.drawDai(100, DAI);
```

* **Params:** amount to draw (in Dai, as string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.drawDai(dai)` withdraws the specified amount of Dai as a loan against the collateral in the CDP. As such, it will fail if the CDP doesn't have enough PETH locked in it to remain at least 150% collateralized.


## **wipeDai**

```javascript
return await cdp.wipeDai(10000000000000000000, DAI.wei);
// or equivalently
return await cdp.wipeDai(100, DAI);
```

* **Params:** amount to repay (in Dai, as string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.wipeDai(dai)` sends Dai back to the CDP in order to repay some (or all) of its outstanding debt.

*Note: CDPs accumulate MKR governance debt over their lifetime. This must be paid when wiping dai debt, and thus MKR must be acquired before calling this method.*

## **freePeth**

```javascript
return await cdp.freePeth(100, PETH);
// or equivalently
return await cdp.freePeth(10000000000000000000, PETH.wei);
```

* **Params:** amount of Peth collateral to free from the CDP, in units defined by the price service.
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.freePeth(peth)` withdraws the specified amount of PETH and returns it to the owner's address. As such, the contract will only allow you to free PETH that's locked in excess of 150% of the CDP's outstanding debt.


## **give**

```javascript
return await cdp.give('0x046ce6b8ecb159645d3a605051ee37ba93b6efcc');
```

* **Params:** Ethereum address (string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.give(address)` transfers ownership of the CDP from the current owner to the address you provide as an argument.


## **shut**

```javascript
return await cdp.shut();
```

* **Params:** none
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.shut()` will close the CDP and return the collateral, in PETH, to its owner. It will fail if the CDP still has outstanding debt.

