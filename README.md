# cerberus-testnet

# inferno-1
Version of cerberus: v2.0.1

chain-id=inferno-1

[config.toml]
persistent_peers = "96e945f29671a62dd23b1228021522cbb91a86f4@116.202.143.90:26656"


#timeout_commit: Please set it up to 29s. I took spare machines with small disks at the moment. We can accelerate later on when we are all onboarded and ready for the votings. 

timeout_commit = "29s"

## instructions for old validators of inferno-1, so you can re-use your node


```
sudo systemctl stop cerberusd
rm -rf ~/cerberus
git clone https://github.com/windpowerstake/cerberus
cd cerberus/
git checkout v2.0.1
make install

cd ~
rm -rf ~/.cerberus/
cerberusd init "yourMonikerNode" --chain-id "inferno-1"
```


Make sure your version is ok:

```cerberusd version```


Must return v2.0.1


## An automation to put your peers in your config.toml file:

```
peers="96e945f29671a62dd23b1228021522cbb91a86f4@116.202.143.90:26656"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.cerberus/config/config.toml
```

Make sure the persistent peer is: `96e945f29671a62dd23b1228021522cbb91a86f4@116.202.143.90:26656`

If this does not work do it manually.

## Reload the genesis for inferno-1

Get your genesis.json file from discord or from here: https://github.com/windpowerstake/cerberus-testnet/blob/main/genesis.json

Or just with the command:

```
rm ~/.cerberus/config/genesis.json
wget https://raw.githubusercontent.com/windpowerstake/cerberus-testnet/main/genesis.json -P ~/.cerberus/config/
```

Verify the shasum:
``` 
jq -S -c -M '' ~/.cerberus/config/genesis.json | sha256sum
#returns 4d0e997e3ba6a555c5c7b39be86d5a2561666fe2b5ac958a0be8a0c80d998128  -
```


When you are ready, make sure to enable cerberus as a daemon (service) and start the service.


testnet is up and running
