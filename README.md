# :palm_tree: Goacoin Wallet Daemon (`goacoind`)

Goacoin Wallet Daemon for headless wallets and masternodes.

## Usage

The container can be either used as a simple headless wallet or a **masternode** only the options used
in the *command* will differ.

### Headless wallet

Run the container and specify at least the `rpcuser` and `rpcpassword` to interact with the Goacoin daemon:
```
docker run wallet -rpcuser=goacoinrpc -rpcpassword=4VvDhcoqFUcZbmkWUMJz8P443WLfoaMmiREKSByJaT4j
```
> We recommend mounting a volume for easier access to the *data* and the *configuration*.
> `docker run lepetitbloc/goacoind -v ./goacoin:/home/goacoin/ -rpcuser=goacoinrpc -rpcpassword=4VvDhcoqFUcZbmkWUMJz8P443WLfoaMmiREKSByJaT4j`

> :warning: Make sur the host directory contains at least an empty, *writable* `data` directory.

### Headless control wallet and masternode

The easiest way to setup **both** at the same is to use `docker-compose`.
Check the provided `docker-compose.yml` as an example and tweak it to your needs!

Then just run:
```
docker-compose up --build
```

> **Pro Tip:** Check the next section for available implementations, that will save you the build step, compose will
just have to pull the images.

## Parent project
This project is part of the `walletd` initiative:
https://github.com/LePetitBloc/walletd

## Parent image
- Berkeley DB v5.3.28.NC
`FROM lepetitbloc/bdb:5.3.28.NC`
> https://github.com/LePetitBloc/bdb/tree/5.3.28.NC
> https://hub.docker.com/r/lepetitbloc/bdb/

## Resources
* https://github.com/goacoincore/goacoin
* https://bitcointalk.org/index.php?topic=2593523.0
* https://goaco.in/

## Licence
MIT
