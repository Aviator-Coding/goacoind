# :palm_tree: Goacoin Wallet Daemon (`goacoind`)

Goacoin Wallet Daemon for headless wallets and masternodes.

## Usage

The container can be either used as a simple headless wallet or a **masternode** only the options used
in the *command* will differ.

### Headless wallet

1. Run the container and specify at least the `rpcuser` and `rpcpassword` to interact with the **Goacoin** daemon:
```
docker run wallet -rpcuser=goacoinrpc -rpcpassword=4VvDhcoqFUcZbmkWUMJz8P443WLfoaMmiREKSByJaT4j
```

> We recommend to mount a volume for easier access to the *data* and the *configuration*.
> You should also create a configuration for your RPC credentials (see `wallet/conf/wallet.conf`) to avoid retyping them when using the `goacoin-cli`.
> ```
> docker run lepetitbloc/goacoind --name goacoin -v ./goacoin:/home/goacoin/`
> ```

> :warning: Make sur the host directory contains at least an empty, *writable* `data` directory.

2. Encrypt your wallet:

docker exec -d goacoin goacoin-cli encryptwallet test
> Wallet encrypted; GoaCoin Core server stopping, restart to run with encrypted wallet. The keypool has been flushed, you need to make a new backup.

docker exec -d goacoin goacoin-cli getaccountaddress ""
GK92mbjS9bCAUuU7DEyyuK9US1qLqkoyce

docker exec -it 5c155e42f591 goacoin-cli -rpcuser=goacoin -rpcpassword=test -rpcport=9998 masternode outputs
{
}

docker exec -it 5c155e42f591 goacoin-cli -rpcuser=goacoin -rpcpassword=test -rpcport=9998 masternode genkey
7ev3RXQXYfztreEz8wmPKgJUpNiqkAkkdxt24C3ZKtg5qEVfou9


### Masternode

## docker

## docker-compose

The easiest way to setup **both** at the same is to use `docker-compose`.
Check the provided `docker-compose.yml` as an example and tweak it to your needs!

```
docker-compose up --build
```

docker exec -it 5c155e42f591 goacoin-cli -rpcuser=goacoin -rpcpassword=test -rpcport=9998 getaccountaddress ""
GK92mbjS9bCAUuU7DEyyuK9US1qLqkoyce

docker exec -it 5c155e42f591 goacoin-cli -rpcuser=goacoin -rpcpassword=test -rpcport=9998 masternode outputs
{
}

docker exec -it 5c155e42f591 goacoin-cli -rpcuser=goacoin -rpcpassword=test -rpcport=9998 masternode genkey
7ev3RXQXYfztreEz8wmPKgJUpNiqkAkkdxt24C3ZKtg5qEVfou9


## Parent project
This project is part of the `walletd` initiative:
https://github.com/LePetitBloc/walletd

## Parent image
- Berkeley DB v5.3.28.NC
`FROM lepetitbloc/bdb:5.3.28.NC`
> https://github.com/LePetitBloc/bdb/tree/5.3.28.NC
> https://hub.docker.com/r/lepetitbloc/bdb/


## Licence
MIT
