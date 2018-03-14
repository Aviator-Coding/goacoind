# Goacoin Wallet Daemon (`goacoind`)
Goacoin Wallet Daemon for headless wallets and **masternodes**. :palm_tree:

## Usage
The container can either be used as a classic headless wallet or a **masternode**, only the *command* arguments will differ.

### Headless wallet
1. Run a **wallet** container and specify at least the `rpcuser` and `rpcpassword` to interact with the **Goacoin** daemon:
```
docker run --name goacoin --restart always -d lepetitbloc/goacoind -rpcuser=goacoinrpc -rpcpassword=4VvDhcoqFUcZbmkWUMJz8P443WLfoaMmiREKSByJaT4j
```
> We recommend to mount a volume for easier access to the *data* and the *configuration* files.
> You should also create a configuration for your RPC credentials (see `wallet/.goacoincore/goacoin.conf`) to avoid retyping them when using the internal `goacoin-cli`.
> ```
> docker run --name goacoin --restart always -d -v ./goacoin:/home/goacoin/ lepetitbloc/goacoind
> ```

> :snake: Ensure that a `data` directory **exists** and is **writable** in the mounted host directory.

2. Once your wallet is running, you can print your main address:
```
docker exec goacoin goacoin-cli getaccountaddress ""
```
> GK92mbjS9bCAUuU7DEyyuK9US1qLqkoyce

2. **Encrypt your wallet:**
> You can use `pwgen` first to generate your *passphrase*:
> ```
> pwgen 32 1
> ```
> quohd4kaw9guvi8ie7phaighawaiLoo6
```
docker exec goacoin goacoin-cli encryptwallet quohd4kaw9guvi8ie7phaighawaiLoo6
```
> Wallet encrypted; GoaCoin Core server stopping, restart to run with encrypted wallet. The keypool has been flushed, you need to make a new backup.

:ocean: Don't forget to **backup** your *passphrase*.

### Masternode

#### Prerequisites
1. You must have received *1000 GOA* on your **wallet** in a **single transaction**, and **must** have waited for, at least, **1 confirmation**.
> **Note1:** If the *1000 GOA* came from multiple transactions, you can send them back to yourself.

> **Note2:** Beware of the transaction cost, you should own *1001 GOA* as a safety measure.

2. Only then you may find the corresponding transaction `hash` and `index` :
```
docker exec goacoin goacoin-cli masternode outputs
```
>```
>{
>  "8e835a7d867d335434925c32f38902268e131e99a5821557d3e77f8ca3829fd8" : "0"
>}
>```

3. Then generate a **masternode** private key:
```
masternode genkey
```
>```
>7ev3RXQXYfztreEz8wmPKgJUpNiqkAkkdxt24C3ZKtg5qEVfou9
>```

4. And finally creates the `~/.goacoincore/masternode.conf` file, and fill in following this template:
> `mn01 masternode:21529 YouMasterNodePrivateKey TransactionHash 0 YourWalletAddress:100`
```
touch ./goacoin/conf/masternode.conf
```

#### Setup
1. As a classic wallet, create a `masternode/.goacoincore/goacoin.conf` configuration file
```
rpcuser=goacoinrpc
rpcpassword=4VvDhcoqFUcZbmkWUMJz8P443WLfoaMmiREKSByJaT4j
masternode=1
masternodeprivkey=7ev3RXQXYfztreEz8wmPKgJUpNiqkAkkdxt24C3ZKtg5qEVfou9
externalip=YOUR.EXTERNAL.IP:1947
addnode=31.132.0.124:1947
addnode=107.174.68.186:1947
addnode=107.175.59.28:1947
addnode=173.212.224.53:1947
addnode=45.43.7.242:1947
addnode=54.37.74.186:1947
addnode=194.67.213.243:1947
```

2. Run a container as a **masternode**:
```
docker run --name masternode --restart always -d -p 1947:1947 -p 1948:1948 -v /home/goacoin/masternode:/home/goacoin/ lepetitbloc/goacoind -masternode=1
```

3. Check the the number of `blocks` until the chain is sync:
```
docker exec masternode goacoin-cli getinfo
```

4. Once the chain synced you can start the **masternode** from your **wallet**:
```
docker exec wallet goacoin-cli masternode start-all
```
> You might need to unlock your **wallet** first:
> ```
>  docker exec wallet goacoin-cli quohd4kaw9guvi8ie7phaighawaiLoo6 60
> ```
> :snake: Mind the **space** before the command below, that's not a typo, it’s meant to avoid storing your passphrase in *history*.

5. Then check the **masternode** status with your initial **transaction hash**:
```
docker exec wallet crowdcoin-cli masternodelist | grep 6d94f70499c3f7ba2c59acaa5c04e54ef123d0e460bb07c55ace6464deaf3c85
```
> `"6d94f70499c3f7ba2c59acaa5c04e54ef123d0e460bb07c55ace6464deaf3c85-1": "ENABLED",`

## docker-compose
You could setup **both** at the same time using `docker-compose`.
Check the provided `docker-compose.yml` as an example and tweak it to your needs!
```
docker-compose up --build
```

## Resources
* Website https://goaco.in/
* Github https://github.com/goacoincore/goacoin
* Bitcointalk announce https://bitcointalk.org/index.php?topic=2593523.0
* Block explorer https://goacoin.be/

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
