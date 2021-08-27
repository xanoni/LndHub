LndHub
======

## Summary

Wrapper for Lightning Network Daemon (`lnd`). It provides separate accounts with minimum
trust required by end users.


## Installation

### Quickstart instructions

```bash
git clone git@github.com:BlueWallet/LndHub.git

cd LndHub && npm install

# please copy or link below two files from the `lnd` folder
ln -si "${LND_DATA_DIR}/data/chain/bitcoin/mainnet/admin.macaroon" ./
ln -si "${LND_DATA_DIR}/tls.cert" ./

# you may want to adjust the default HOST:PORT settings (e.g., set
# host to 'localhost' instead in Tor-only LndHub setups)
export HOST='0.0.0.0' && export PORT=3000

# please configure `redis` and update `config.js` before starting LndHub
npm start
```

### Additional installation notes

Install `bitcoind`, `lnd`, and `redis`. Edit LndHub's `config.js` to set it up correctly.
Copy the files `admin.macaroon` (for Bitcoin mainnet, usually stored in
`~/.lnd/data/chain/bitcoin/mainnet/admin.macaroon`) and `tls.cert` (usually stored in
`~/.lnd/tls.cert`) into the root folder of LndHub.

LndHub expects `lnd`'s wallet to be unlocked. Otherwise, it will attempt to unlock it
with the password stored in `config.lnd.password`.

Don't forget to configure disk-persistence for `redis` (e.g., you may want to set `appendonly`
to `yes` in `redis.conf` (see http://redis.io/topics/persistence for more information).

If you have no `bitcoind` instance, for example because you use `neutrino`, or you have
no `bitcoind` wallet, for example because you use `lnd` for wallet management, you can remove
all `bitcoind`-related settings from `config.js`.

Please note that this feature is limited to Bitcoin, so you can't use it if you use any
other cryptocurrency with `lnd` (e.g., Litecoin).

### Third-party guides

You can use the below two guides if above instructions were not sufficiently clear:

* https://github.com/dangeross/guides/blob/master/raspibolt/raspibolt_6B_lndhub.md
* https://medium.com/@jpthor/running-lndhub-on-mac-osx-5be6671b2e0c

Please note that some of the steps described are not strictly necessary. For example, `babel`
should not be called manually. Please see our quickstart instructions from above instead.

### Deployment to Heroku

Set the below three config vars:

* `CONFIG`: json-serialized config object
* `MACAROON`: hex-encoded `admin.macaroon`
* `TLSCERT`: hex-encoded `tls.cert`

### Running LndHub in Docker

LndHub is available on Docker Hub as [`bluewalletorganization/lndhub`](https://hub.docker.com/r/bluewalletorganization/lndhub).

Please note that this requires a separate instance of redis and `lnd` and optionally, `bitcoind`.

You can also view Umbrel's implementation using `docker-compose`, see:

* https://github.com/getumbrel/umbrel/blob/280c87f0f323666b1b0552aeb24f60df94d1e43c/apps/lndhub/docker-compose.yml


## Reference client implementation

LndHub can be used in ReactNative or Node.js environments. Please find an example below:

* https://github.com/BlueWallet/BlueWallet/blob/master/class/wallets/lightning-custodian-wallet.js


## Testing

Acceptance tests can be found below:

* https://github.com/BlueWallet/BlueWallet/blob/master/LightningCustodianWallet.test.js

![image](https://user-images.githubusercontent.com/1913337/52418916-f30beb00-2ae6-11e9-9d63-17189dc1ae8c.png)


## Responsible disclosure

Found critical bugs/vulnerabilities? Please email them to bluewallet@bluewallet.io.

Thank you!
