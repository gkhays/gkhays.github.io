---
layout: post
title: Blockchain Transactions
categories: [ethereum, bitcoin]
---

The purpose of this project is to demonstrate the ability to record identity-related transactions on a private blockchain. The idea is to record actions or events associated with resources with which an identity may interact, typically called entitlements.

I started with the [Ethereum Project](https://www.ethereum.org/) since it supports so called "`smart contracts`" and was designed for uses other than pure digital cash transactions as is the case with Bitcoin. I chose the Golang implementation, [go-ethereum](https://github.com/ethereum/go-ethereum).

### Running in Docker ###

In order to get up and running quickly, I used a Docker container with `go-ethereum` already installed. The first step is to retrieve the image from DockerHub.

`docker pull ethereum/client-go`

Start a node with the JSON-RPC interface listening on port 8545.

`docker run -it -p 8545:8545 -p 30303:30303 ethereum/client-go --rpc --rpcaddr "0.0.0.0"`

https://github.com/ethereum/go-ethereum/wiki/Running-in-Docker

### Docker Compose ###

Create a docker-compose file with the settings above.
```yaml
# docker-compose up -d

geth:
    container_name: client-go
    image: ethereum/client-go
    ports:
        - "8545:8545"
        - "30303:30303"
    command: --rpc --rpcaddr "0.0.0.0" --rpcapi "db,eth,net,web3" --rpccorsdomain "*" --testnet --nodiscover
```

Bring the container up: `docker-compose up -d`.
```bash
~\src\ethereum [master ≡ +1 ~0 -0 !]> docker ps
CONTAINER ID        IMAGE                COMMAND             CREATED              STATUS              PORTS                                              NAMES
21189ed24134        ethereum/client-go   "/geth"             About a minute ago   Up About a minute   0.0.0.0:8545->8545/tcp, 0.0.0.0:30303->30303/tcp   client-go
~\src\ethereum [master ≡ +1 ~0 -0 !]> docker exec -it 21189ed24134 /bin/bash
root@21189ed24134:/# ls
bin  boot  dev  etc  geth  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

Confirm the server is running with the intended switches.
```bash
root@20c354e83cf1:/# ps aux
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root          1  0.3  3.0 326624 61820 ?        Ssl  19:09   0:01 /geth --rpc --rpcaddr 0.0.0.0 --rpcapi db,eth,net,web3
root         13  0.0  0.1  18240  3388 ?        Ss   19:11   0:00 /bin/bash
root         41  0.0  0.1  34424  2760 ?        R+   19:14   0:00 ps aux
```

Attach to the console.
```bash
root@21189ed24134:/# ./geth attach
Welcome to the Geth JavaScript console!

instance: Geth/v1.5.8-stable-f58fb322/linux/go1.6.2
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

>
```

## Ethereum Quick Start

Below is a quick bash script to start go-ethereum. The default ports are fine.

RPC Port: default: 8545<br/>
Port default: 30303

```bash
# geth.sh
# Fetch local IP address into a variable.
MY_IP=$(ip addr list enp0s25 | grep "inet " | cut -d' ' -f6 | cut -d/ -f1)

# --testnet and --dev are mutually exclusive
~/src/ethereum/go-ethereum/build/bin/geth \
  --testnet --identity "IGBlock" \
  --rpc --rpcaddr "$MY_IP" --rpccorsdomain "*" \
  --nodiscover --rpcapi "db,eth,net,web3" console
```

This creates a blockchain on the Ethereum `TEST-NET`. It is possible to create a private blockchain as well using the `--networkid 1999` switch. See [Setting up a local private testnet](https://github.com/ethereum/homestead-guide/blob/master/source/network/test-networks.rst#geth-go-client-1) for more detail.

### REST Client
Since go-ethereum supports a JSON-RPC interface, I use the Chrome DHC extension (similar to Postman) as a RESTful client.

![DHC](/images/dhc-rest-go-ethereum.png)

### Mist
Ethereum also supports a rich, native client based on [Meteor](https://www.meteor.com/) called [Mist](https://github.com/ethereum/mist). You may recognize Meteor as the Rocket.Chat native application is based on it as well.

To get Mist to connect to your private blockchain, use the `--rpc` command line switch, e.g.

```bat
Mist.exe --rpc http://10.45.14.31:8545
```

Windows users may set up a shortcut for the `Mist` application.

![Shortcut](/images/mist-win-shortcut.png)

Here you can see the blockchain and the `Ether` that has been "mined" so far.

![Mist](/images/mist-client.png)
