`sudo systemctl stop uptickd`  
`uptickd unsafe-reset-all`  
`nano $HOME/.uptickd/config/app.toml`  
```
snapshot-interval = 2000
snapshot-keep-recent = 10

pruning = "custom"

pruning-keep-recent = "5"
pruning-keep-every = "0"
pruning-interval = "10"
```
`nano $HOME/.uptickd/config/config.toml`  
```
indexer = "null"
```
`SEEDS="7aad751eb956d65388f0cc37ab2ea179e2143e41@seed0.testnet.uptick.network:26656,7e6c759bcf03641c65659f1b9b2f05ec9de7391b@seed1.testnet.uptick.network:26656"`  
`SNAP_RPC="http://peer1.testnet.uptick.network:26657"`  
`SNAP_RPC_2="http://peer1.testnet.uptick.network:26657"`  
```
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 5000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
```
`echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH`  
```
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC_2\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"$SEEDS\"|" $HOME/.uptickd/config/config.toml
```
`sudo systemctl restart uptickd`  
`journalctl -u uptickd -f`  
