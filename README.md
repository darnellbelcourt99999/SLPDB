
# SLPDB

SLPDB is a persistance layer for SLP token transactions.

### NOTICE: SLPDB is in an alpha state.  Expect changes.

### How to use SLPDB: 

1) Get mongodb running locally, e.g.,:
`docker run -d -p 27017:27017 -v <your-absolute-path-to-data>:/data/db mongo`

2) Get bitcoind rpc connection running locally, set `user`, `pass`, and `port` in `config.ts`

3) Install deps: `npm install`

4) Start SLPDB: `npm start`, and then wait for sync process to complete (after console stops updating).
    * First SLPDB will need to sync all SLP transactions since SLP started
    * Second SLPDB will build token graphs for each token

5) In another console, run example query script: `node ./examples/addresses.js`

6) Make SLP transactions and see the information update for the particular token, check that the db addresses updated properly.

### NOTES

* `rpcworkqueue` within bitcoin.conf should be set to something large, try `rpcworkqueue=1000`.

* The following are being calculated and updated in real-time:
    - `qty_valid_txns_since_genesis`
    - `qty_valid_token_utxos`
    - `qty_valid_token_addresses`
    - `qty_token_circulating_supply`
    - `qty_token_burned`
    - `qty_token_minted`
    - `qty_satoshis_locked_up`

* The following stats are not being computed yet:
    - `block_created`
    - `block_last_active_mint`
    - `block_last_active_send`