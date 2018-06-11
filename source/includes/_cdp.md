# CDP

Now that you've used `maker` to either open a new CDP or retrieve an existing one, you can use the returned `cdp` object to call functions on it.

## **getCdpId**

```javascript
const id = await cdp.getCdpId();
```

* **Params:** none
* **Returns:** promise (resolves to CDP ID)

Use `cdp.getCdpId()` to retrieve the ID from a CDP object. You may need to use the ID as a parameter for other functions.


## **getInfo**

```javascript
const info = await cdp.getInfo();
const lockedPeth = info.ink;
```

* **Params:** none
* **Returns:** promise (resolves to CDP info object)

`cdp.getInfo()` will return a few distinct properties of the CDP:

* lad: The Ethereum address associated with the owner of the CDP
* ink: Amount of collateral locked in the CDP
* art: Outstanding normalized debt (tax only)
* ire: Outstanding normalized debt

Please refer to the [MakerDAO White Paper](https://makerdao.com/whitepaper/DaiDec17WP.pdf) or reach out on our [community chat](https://chat.makerdao.com/home) if you need help understanding how these variables are used in the system.


## **getCollateralAmount**

```javascript
const lockedPeth = await cdp.getCollateralAmount();
```

* **Params:** none
* **Returns:** promise (resolves to locked amount in PETH)

`cdp.getCollateralAmount()` returns the amount of locked collateral in the CDP.


## **getDebtAmount**

```javascript
const daiDebt = await cdp.getDebtAmount();
```

* **Params:** none
* **Returns:** promise (resolves to the amount of outstanding debt in Dai)

`cdp.getDebtAmount()` returns the amount of Dai that has been borrowed against the collateral in the CDP.


## **lockEth**

```javascript
return await cdp.lockEth('0.1');
```

* **Params:** amount to lock in the CDP (in ETH, as string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.lockEth(eth)` abstracts the token conversions needed to lock collateral in a CDP. It first converts the ETH to WETH, then converts the WETH to PETH, then locks the PETH in the CDP.


## **drawDai**

```javascript
return await cdp.drawDai('100');
```

* **Params:** amount to draw (in Dai, as string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.drawDai(dai)` withdraws the specified amount of Dai as a loan against the collateral in the CDP. As such, it will fail if the CDP doesn't have enough PETH locked in it to remain at least 150% collateralized.


## **wipeDai**

```javascript
return await cdp.wipeDai('100');
```

* **Params:** amount to repay (in Dai, as string)
* **Returns:** promise (resolves to `transactionHybrid`)

`cdp.wipeDai(dai)` sends Dai back to the CDP in order to repay some (or all) of its outstanding debt.

*Note: CDPs accumulate MKR governance debt over their lifetime. This must be paid when wiping dai debt, and thus MKR must be acquired before calling this method.*

## **freePeth**

```javascript
return await cdp.freePeth('0.1');
```

* **Params:** amount to withdraw (in PETH, as string)
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

