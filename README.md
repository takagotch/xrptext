### xrptext
---
https://xrptext.com/

https://github.com/WietseWind/xrp-text

```js
// src/connectRippled.js
'use strict'

const EventEmitter = require('event')
const RippleClient = require('rippled-ws-client')
const RippleSign = require('rippled-ws-client-sign')

class ConnectRippled extends EventEmitter {
  constructor (config) {
    let ledger
    
    super()
    
    return new Promise((resolve, reject) => {
      console.log()
      new RippleClient(config.ripple.server).then((Connection) => {
        Object.assign(this, {
          withdraw: (toWallet, toDtag, amount) => {
            return new RippleSign({
              TransactionType: 'Payment',
              Account: config.ripple.account,
              Destination: toWallet,
              DestinationTag: toDtag,
              Amount: amount * 10000000,
              LastLedgerSequence: ledger + 15
            }, config.ripple.keypair, Connection)
          }
        })
        
        Connection.on('error', (e) => {})
        Connection.on('reconnect', (r) => {})
        Connection.on('')
      })
    })
  }
}
```

```
node index.js
npm run dev
```

```
```


