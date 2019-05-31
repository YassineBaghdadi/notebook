# Ethereum

## Setup Node

```bash
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository -y ppa:ethereum/ethereum
$ sudo apt-get update
$ sudo apt-get install ethereum
```

## Create a new wallet

```js
const EthWallet = require("ethereumjs-wallet")
const bip39 = require("bip39")
const hdkey = require("ethereumjs-wallet/hdkey")

// Generate mnemonic and seed
const mnemonic = bip39.generateMnemonic()
const seed = bip39.mnemonicToSeed(mnemonic)

console.log(`generated mnemonic: ${mnemonic}\n`)

const hdwallet = hdkey.fromMasterSeed(mnemonic)
const walletHdPath = "m/44'/60'/0'/0/"
const wallet = hdwallet.getWallet()
const privateKey = wallet.getPrivateKey().toString("hex")

console.log("address:", wallet.getAddress().toString("hex"))
console.log("private key", privateKey)
console.log("filename", wallet.getV3Filename(Date.now()))

console.log(wallet.toV3("he-yo"))
```

## Restore Wallet

```js
const EthWallet = require("ethereumjs-wallet")
const hdkey = require("ethereumjs-wallet/hdkey")

// by pk
const wallet = EthWallet.fromPrivateKey(
  Buffer.from(
    `${privateKey}`,
    "hex"
  )
)

console.log("address:", wallet.getAddress().toString("hex"))

// by seed
const hdws = hdkey.fromMasterSeed(
  `${seed}`
)

const ws = hdws.getWallet()

console.log("address:", ws.getAddress().toString("hex"))

// by keystore
const v3 = ""
const pwd = ""
const ksw = EthWallet.fromV3(v3, pwd)
console.log("address:", ksw.getAddress().toString("hex"))

```