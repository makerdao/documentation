# Token Conversion

```javascript
const conversionService = maker.service('conversion');
```
Get the token conversion service with maker.service('conversion').

The token conversion service offers functions to convert between Eth, Weth and Peth, handling allowances when necessary.

## **convertEthToWeth**

```javascript
return await conversionService.convertEthToWeth(10);
```

* **Params:** amount of Eth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertEthToWeth` deposits ETH into the WETH contract

## **convertWethToPeth**

```javascript
return await conversionService.convertWethToPeth(10);
```

* **Params:** amount of Weth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertWethToPeth()` joins WETH into PETH, first giving token allowance if necessary

*Note: this process is not atomic if a token allowance needs to be set, so it's possible for one of the transactions to succeed but not both.  See [Using DsProxy](#proxy-service) for executing multiple transactions atomically.*

## **convertEthToPeth**

```javascript
return await conversionService.convertEthToPeth(10);
```

* **Params:** amount of Eth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertEthToPeth()` awaits `convertEthToWeth`, then calls `convertWethToPeth`

*Note: this process is not atomic, so it's possible for some of the transactions to succeed but not all.  See [Using DsProxy](#proxy-service) for executing multiple transactions atomically.*

## **convertWethToEth**

```javascript
return await conversionService.convertconvertWethToEth(10);
```

* **Params:** amount of Weth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertWethToEth` withdraws Eth from Weth contract

## **convertPethToWeth**

```javascript
return await conversionService.convertPethToWeth(10);
```

* **Params:** amount of Peth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertPethToWeth()` exits PETH into WETH, first giving token allowance if necessary

*Note: this process is not atomic if a token allowance needs to be set, so it's possible for one of the transactions to succeed but not both.  See [Using DsProxy](#proxy-service) for executing multiple transactions atomically.*

## **convertPethToEth**

```javascript
return await conversionService.convertPethToEth(10);
```

* **Params:** amount of Peth to convert
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`convertPethToEth()` awaits `convertPethToWeth`, then calls `convertWethToEth`

*Note: this process is not atomic, so it's possible for some of the transactions to succeed but not all.  See [Using DsProxy](#proxy-service) for executing multiple transactions atomically.*
