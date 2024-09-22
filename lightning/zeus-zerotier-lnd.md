# Connect Zeus with ZeroTier to LND
A checklist to connect the [Zeus](https://zeusln.com/) app with [ZeroTier](https://my.zerotier.com/) to the lighning node [LND](https://docs.lightning.engineering/lightning-network-tools/lnd).

## 1 Sign up at zerotier and create a network
- visit https://my.zerotier.com
- sign up
- create a network and you get a `network-id`

## 2 Install zerotier on your lnd node and join the network
- log in with `ssh` to your node
- visit https://www.zerotier.com/download/
- go to linux and copy the desired install command
- paste and execute the install command on your node
- you got a `zerotier-address` for the lnd node
- test the zerotier-cli `sudo zerotier-cli info`
- join the network with the node `sudo zerotier-cli join network-id`

## 3 Authorize the lnd node to the network
- visit https://my.zerotier.com
- select the network with the `network-id`
- auth the `zerotier-address` of the lnd node
- you get a `managed-ip` for the lnd node

## 4 Configure and restart lnd
- locate `lnd.conf` on your node `sudo find . -name lnd.conf`
- edit `lnd.conf` with vi or nano
- add an additional `tlsextraip=managed-ip` line
- save and exit `lnd.conf`
- restart lnd

## 5 Install zerotier on your mobile device and join the network
- install `ZeroTier One` from the app store
- start the app and you will see the `zerotier-address` for the device at the bottom
- press add network and scan the `network-id` on `my.zerotier.com`
- press add

## 6 Authorize the mobile device to the network and connect
- auth the `zerotier-address` of the mobile device on `my.zerotier.com`
- connect in the app to the network with the `toggle switch` on the right side

## 7 Configure zeus and connect with zerotier to lnd
- open the nodes in the zeus app
- open an existing tor node config or add an new one
- duplicate the tor node config
- change the host to `https://managed-ip` of the lnd node
- use tor `no`
- certificate validation `no`
- press save node config
- connect

## Sources
- https://docs.zerotier.com/start
- https://tutorials.lightningnode.info/zerotier/
- https://darthcoin.substack.com/p/tailscale-tunnel-zu-deiner-node-aufsetzen

[/](./../readme.md)
