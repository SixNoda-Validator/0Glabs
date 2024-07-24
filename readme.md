# 0G labs - Setup Validator Node

## Install Dependencies
Ensure you have the necessary dependencies installed, such as Go and Node.js. Instructions for installing these can be found in the official 0G documentation.

## Download and Install the Source Code
```
git clone https://github.com/0g/0g-chain.git
cd 0g-chain
make install
```
## Initialize the Node
Initialize your node with the following command:

```
0gd init sixnode --chain-id 0g-chain
```
## Configure the Configuration Files
Open the config.toml file for editing:

```
nano ~/.0g/config/config.toml
```
Make the following changes:

Set the moniker:

```
moniker = "sixnode"
```
Set persistent_peers if you have a list of peers to connect to:
```
persistent_peers = "<peers>"
```
Set your IP address and port:
```
external_address = "159.69.138.44:8545"
```
## Create or Restore the Validator Key
Create a new validator key or restore an existing one:

```
0gd keys add sixnode
# or restore an existing key
0gd keys add sixnode --recover
```

## Create the Validator Transaction
Create a transaction to set up your validator:

```
0gd tx staking create-validator \
  --amount=1000000u0g \
  --pubkey=$(0gd tendermint show-validator) \
  --moniker="sixnode" \
  --chain-id=0g-chain \
  --from=sixnode \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --gas=auto
```
## Start the Node
Start your node with the following command:

```
0gd start
```
Now your validator should be up and running, synchronizing with the network. Ensure that your node is operating correctly by checking the logs:

```
tail -f ~/.0g/logs/0gd.log
```
