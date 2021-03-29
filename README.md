The node needs to be synced at least to mary era for this to work. The `payment-address` needs to have at least some funds for the fee.

## Set node socket path
```
export CARDANO_NODE_SOCKET_PATH=/home/gabriel/repos/cardano/my-node/db/node.socket
```

## Create voting key registration transaction with fixed address
```
~/Downloads/voter-registration \
  --payment-signing-key payment_ext.skey \
  --stake-signing-key stake_ext.skey \
  --vote-public-key vote_bech32.pub \
  --payment-address "addr_test1qzq0nckg3ekgzuqg7w5p9mvgnd9ym28qh5grlph8xd2z92sj922xhxkn6twlq2wn4q50q352annk3903tj00h45mgfmsu8d9w5" \
  --testnet-magic 1097911063 \
  --out-file voter-registration.txsigned
```

## Create voting key registration transaction with derived address
```
~/Downloads/voter-registration \
  --payment-signing-key payment_ext.skey \
  --stake-signing-key stake_ext.skey \
  --vote-public-key vote_bech32.pub \
  --payment-address "$(cardano-cli address build --payment-verification-key-file payment_ext.vkey --stake-verification-key-file stake.vkey --testnet-magic 1097911063)" \
  --testnet-magic 1097911063 \
  --out-file voter-registration.txsigned
```

## Run node
```
cardano-node run \
  --topology testnet-topology.json \
  --database-path ./db \
  --socket-path ./db/node.socket \
  --host-addr 127.0.0.1 \
  --port 3001 \
  --config testnet-config.json
```

## Check nodes running
```
cardano-cli query tip --testnet-magic 1097911063
```
