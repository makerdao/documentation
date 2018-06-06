# Maker

Once you've connected your instance of `maker` (following the instructions in the `Web3Service` section), you can use the `maker` interface to access the core library functionality.

## **service**
* **Params:** service (string)
* **Returns:** service object

The service function can be used to access services that were injected into your instance of `maker`. The service must be in the list of available services you passed to `ConfigFactory`.

*Note: see the `Custom Config Files` section further down for an example config file with a list of services*

```javascript
const priceFeedService = maker.service('priceFeed');
```

## **openCdp**
* **Params:** none
* **Returns:** promise (resolves to new CDP object)

`maker.openCdp()` will create a new CDP, and then return the CDP object, which can be used to access other CDP functionality.

By default, the promise will resolve when the transaction is mined.

```javascript
const newCdp = await maker.openCdp();
```

## **getCdp**

* **Params:** CDP ID (integer)
* **Returns:** promise (resolves to CDP object)

`maker.getCdp(id)` creates a CDP object for an existing CDP. The CDP object can then be used to interact with your CDP.

```javascript
const cdp = await maker.getCdp(614);
```