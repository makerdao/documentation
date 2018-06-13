# Configuration

## Web3 settings

```javascript
{
	"usePresetProvider": true,
	"provider": {
	  "type": "INFURA",
	  "network": "kovan"
	  "infuraApiKey": 'ab...yz'
	},
	"privateKey": "0x..."
 }
```

A common service to pass in settings to is the Web3Service, which controls

1. How the library connects to an ethereum node
2. Which private keys the library has access to

For example, these are the Web3Service settings for the "kovan" config file from above

Below are the different options that can be passed in to the Web3Service settings

### usePresetProvider

```javascript
"usePresetProvider": true
```

if marked true, the object obtained from `window.web3` (if there is one) will be used as the Provider, instead of creating a new one. For example, this should be true if the library is used in a browser and it should use metamask as its Web3Provider.

Default value: false.

### statusTimerDelay

```javascript
"statusTimerDelay": 2000

```

Number in milliseconds that represents how often the blockchain connection and account authentication is checked. This allows the library to move out of an authenticated or connected state when it discovers it no longer has access to unlocked accounts, or can no longer connect to a node.

default value: 5000 (5 seconds)

### privateKey

```javascript
privateKey: "0x..."
```
private key used to sign all transactions.  If not provided, the first account available from the ethereum node will be used to sign transaction.

### Provider Type

```javascript
"provider": {
  "type": "HTTP"
}
```

"INFURA": connect to an ethereum node via infura

"TEST": connect to a local test blockchain at 'http://127.1:2000'

"HTTP": connect to an ethereum node via any arbitrary url

### Provider Network

```javascript
"provider": {
  "network": "kovan"
}
```
Name of ethereum network to use when using the "INFURA" provider type.  The Maker smart contracts are only deployed on mainnet and kovan (not ropsten or rinkeby)

options: "mainnet" | "kovan"

### Provider URL

```javascript
"provider": {
  type: "HTTP"
  url: 'https://sai-service.makerdao.com/node'
}

```
url of node to connect.  Only used when using "HTTP" provider type.

### Infura API Key

```javascript
"provider": {
  type: "INFURA"
  infuraApiKey: 'ab...yz'
}

```
String value of your Infura unique Access Token (the part after infura.io/ when accessing infura via https)

### Default Web3Service Settings

```javascript
{
  usePresetProvider: true,
  provider: {
    type: "HTTP",
    url: 'https://sai-service.makerdao.com/node'
  }
};
```

if no settings are passed in to the Web3Service in the config json file, the default settings are used.  It connects to a node run by the Maker team at "https://sai-service.makerdao.com/node"
