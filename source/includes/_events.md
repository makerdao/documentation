# Events

The event pipeline allows developers to easily create real-time applications by letting them listen for important state changes and lifecycle events.

### Wildcards

An event name passed to any event emitter method can contain a wildcard (the `*` character). A wildcard may appear as `foo/*`, `foo/bar/*`, or simply `*`.

`*` matches one sub-level.

e.g. `price/*` will trigger on both `price/USD_ETH` and `price/MKR_USD` but not `price/MKR_USD/foo`.

`**` matches all sub-levels.

e.g. `price/**` will trigger on `price/USD_ETH`, `price/MKR_USD`, and `price/MKR_USD/foo`.

### Event Object

```javascript
{
    type: <event_type>,
    payload: <event_payload>, /* if applicable */
    index: <event_sequence_number>,
    block: <latest_block_when_emitted>
}
```

Triggered events will recieve the object shown on the right.

* `<event_type>` - the name of the event
* `<event_payload>` - the new state data sent with the event
* `<event_sequence_number>` - a sequentially increasing index
* `<latest_block_when_emitted>` - the current block at the time of the emit

## Maker Object


### `Price`

```javascript
maker.on('price/ETH_USD', eventObj => {
    const { price } = eventObj.payload;
    console.log('ETH price changed to', price);
})
```


Event Name        | Payload
----------        | --------------
`price/ETH_USD`   | { price }
`price/MKR_USD`   | { price }
`price/WETH_PETH` | { ratio }


### `Web3`


```javascript
maker.on('web3/AUTHENTICATED', eventObj => {
    const { account } = eventObj.payload;
    console.log('web3 authenticated with account', account);
})
```

Event Name            | Payload
----------            | --------------
`web3/INITIALIZED`    | { provider: { type, url } }
`web3/CONNECTED`      | { api, network, node }
`web3/AUTHENTICATED`  | { account }
`web3/DEAUTHENTICATED`| { }
`web3/DISCONNECTED`   | { }


## CDP Object

```javascript
cdp.on('DEBT', eventObj => {
    const { dai } = eventObj.payload;
    console.log('Your cdp is now has a dai debt of', dai);
})
```

Event Name   | Payload
------------ | --------------
`COLLATERAL` | { USD, ETH }
`DEBT`       | { dai }
