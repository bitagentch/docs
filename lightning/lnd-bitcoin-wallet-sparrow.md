# Open a LND Bitcoin Wallet in Sparrow

## 1 Introduction
When you use the Lightning Network Daemon [lnd](https://github.com/lightningnetwork/lnd), you have an [aezeed](https://github.com/lightningnetwork/lnd/tree/master/aezeed) mnemonic sentence (24 words) for backup.  
`aezeed` is an advanced form of the [bip39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) mnemonic sentence.  
If you want to use your backup, you can't import it in any Bitcoin Wallet, because they usually only support `bip39`.  
The only wallet i know, that supports the import of an `aezeed` mnemonic sentence is [BlueWallet](https://bluewallet.io/), but they don't support [Taproot](https://github.com/bitcoin/bips/blob/master/bip-0086.mediawiki) addresses yet.  

## 2 aezeed Decoder
[Sparrow](https://www.sparrowwallet.com/) Wallet supports the import of a [bip32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) master private key.  
And [Guggero](https://github.com/guggero) has written a [decoder](https://guggero.github.io/cryptography-toolkit/#!/aezeed) for an `aezeed` mnemonic sentence to a `bip32` master private key.  
To use the decoder it is better to [clone](https://github.com/guggero/cryptography-toolkit) it and open the `index.html` local in your browser.  

## 3 aezeed generate / decode Example
When you [generate](https://guggero.github.io/cryptography-toolkit/#!/aezeed) an `aezeed` mnemonic sentence with the following parameters
- aezeed version `0`
- Internal version `1`
- Birthday `0`
- No Passphrase
- Entropy `00000000000000000000000000000000`
- Salt `0000000000` 

you will get the following 24 words
```
abstract essay woman staff seminar culture neck grunt notable work between torch mandate loud stomach eager deer object abandon abandon abandon ancient pole avocado
```
and the `bip32` master private key 
```
xprv9s21ZrQH143K2JbpEjGU94NcdKSASB7LuXvJCTsxuENcGN1nVG7QjMnBZ6zZNcJaiJogsRaLaYFFjs48qt4Fg7y1GnmrchQt1zFNu6QVnta
```
And when you decode this `aezeed` mnemonic sentence, you will the get same parameters and the same `bip32` master private key back.

## 4 LND Bitcoin Wallets
When you run the LND `lncli wallet accounts list` command, you will see a list of accounts:
```
{
    "accounts": [
        {
            "name": "default",
            "address_type": "HYBRID_NESTED_WITNESS_PUBKEY_HASH",
            "extended_public_key": "ypub...",
            "derivation_path": "m/49'/0'/0'",
            ...
        },
        {
            "name": "default",
            "address_type": "WITNESS_PUBKEY_HASH",
            "extended_public_key": "zpub...",
            "derivation_path": "m/84'/0'/0'",
            ...
        },
        {
            "name": "default",
            "address_type": "TAPROOT_PUBKEY",
            "extended_public_key": "xpub...",
            "derivation_path": "m/86'/0'/0'",
            ...
        },
        ...
    ]
```
From the `bip32` master private key are three LND Bitcoin Wallets derived
- `m/49'/0'/0'` [bip49](https://github.com/bitcoin/bips/blob/master/bip-0049.mediawiki) Nested Segwit `P2SH-P2WPKH`
- `m/84'/0'/0'` [bip84](https://github.com/bitcoin/bips/blob/master/bip-0084.mediawiki) Native Segwit `P2WPKH`
- `m/86'/0'/0'` [bip86](https://github.com/bitcoin/bips/blob/master/bip-0086.mediawiki) Taproot `P2TR`

With the `bip32` master private key and the derivation path we have all the information needed to open LND Bitcoin Wallets in Sparrow.  

Note that there is also for every wallet the Extended Public Key `xpub`, which can be useful to open Watch Only Wallets without the aezeed decoding.  
You may also use the `xpub` to check the openend LND Bitcoin Wallet in Sparrow.

## 5 Open a LND Bitcoin Wallet in Sparrow
To open a LND Bitcoin Wallet in Sparrow you click `File` `New Wallet`.  
Then you have to enter a wallet name and press `Create Wallet`.  
In the Settings you choose the desired `Script Type`, `Taproot (P2TR)`, for example.  
Now you click under Keystores on `New or Imported Software Wallet`.  
There you press on `Enter Private Key` near Master Private Key (Bip32).  
Then you enter the `bip32` master private key and click on `Import`.  
Now you click on `Import Keystore` and press `Apply`.  
You may enter a Password or just click `No Password`.  
Your LND Bitcoin Wallet is now open in Sparrow.

## 6 Check a LND Bitcoin Wallet in Sparrow
You may check the opened LND Bitcoin Wallet with the `xpub` from above or you use the `lncli wallet addresses list` command and check some addresses.  
When you have a transaction history or funds on the wallet you see also wheter it is correct or not.


## Sources
- https://danielabrozzoni.com/posts/import-aezeed-seed-into-sparrow/
