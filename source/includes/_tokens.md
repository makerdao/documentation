# Tokens

```javascript
const tokenService = maker.service('token');
const dai = tokenService.getToken('DAI');
```
Get a token object through the getToken(tokenSymbol) function on the tokenService

Here's the list of tokens that can be passed into getToken(): 'DAI', 'MKR', 'WETH', 'PETH', 'ETH' (can also be obtained with `tokenService.getTokens()`).  
A [currency unit](https://makerdao.com/documentation/#units) can also be passed into `getTokens()` instead 

The below methods can be called on any token object.  Dai is used as an example, but they apply to all tokens

## **allowance**

```javascript
const allowance = await dai.allowance('0x...owner', '0x...spender');
```

* **Params:**
	* `tokenOwner` - address of token owner
	* `spender` - address of token spender
* **Returns:** promise (resolves to token allowance)

`allowance()` returns a [currency unit](https://makerdao.com/documentation/#units) representing the token allowance

## **balance**

```javascript
const balance = await dai.balance();
```

* **Params:** none
* **Returns:** promise (resolves balance of current account)

`balance()` returns a [currency unit](https://makerdao.com/documentation/#units) representing the token balance of the current account

## **balanceOf**

```javascript
const balanceOf = await dai.balanceOf('0x...f00');
```

* **Params:** address to check
* **Returns:** promise (resolves balance of address)

`balance()` returns a [currency unit](https://makerdao.com/documentation/#units) representing the token balance of the supplied account

## **totalSupply**

```javascript
const totalSupply = await dai.totalSupply();
```

* **Params:** none
* **Returns:** promise (resolves total supply of token)

`balance()` returns a [currency unit](https://makerdao.com/documentation/#units) representing the total token supply

## **approve**

```javascript
return await dai.approve('0x...f00', 10000);
```

* **Params:** 
	* `spender` - address of token spender
	* `amount` - amount of token to allow
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`approve()` approves the spending address to spend up to `amount` of `msg.sender`'s tokens

## **approveUnlimited**

```javascript
return await dai.approveUnlimited('0x...f00');
```

* **Params:** address of token spender
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`approveUnlimited()` approves the spending address to spend the maximum amount of `msg.sender`'s tokens

## **transfer**

```javascript
return await dai.transfer('0x...f00', 100);
```

* **Params:** 
	* `to` - address to send to
	* `amount` - amount of token to send
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`transfer()` transfers `amount` of token to `to` address

## **transferFrom**

```javascript
return await dai.transferFrom('0x...fr0m', '0x...t0', 100);
```

* **Params:** 
	* `from` - address to send tokens from
	* `to` - address to send to
	* `amount` - amount of token to send
* **Returns:** promise (resolves to [`transactionObject`](#transactions) once mined)

`transferFrom()` transfers `amount` of token from `from` address to `to` address. Transaction will fail if `msg.sender` does not have allowance to transfer the amount of tokens from the `from` address.
