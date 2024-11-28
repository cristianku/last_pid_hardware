# Mellanox Configuration
#### Assign the Correct IP Address
```yaml
sudo ip addr add 192.168.200.120/24 dev enp4s0f0np0
sudo ip route add default via 192.168.200.1
```

#### Add a new persistent configuration:

```
sudo nmcli connection add type ethernet con-name Mellanox10G ifname enp4s0f0np0 ip4 192.168.200.120/24 gw4 192.168.200.1
sudo nmcli connection up Mellanox10G
```
### Persistent Configuration Check:
```yaml
ip addr show enp4s0f0np0
```

### MTU Settings (Optional): 
For optimizing 10Gbps performance, consider increasing the MTU size if your network supports jumbo frames:

```yaml
sudo ip link set dev enp4s0f0np0 mtu 9000
```

### Check the MTU if it has been set :
```yaml
mtu 9000
```

```
cristianku@localhost:~$ ip link show enp4s0f0np0
3: enp4s0f0np0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9000 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 9c:dc:71:5f:d0:b0 brd ff:ff:ff:ff:ff:ff
cristianku@localhost:~$ 
```

### Verify the configuration 
```yaml
cristianku@localhost:~$ ethtool enp4s0f0np0

Settings for enp4s0f0np0:
	Supported ports: [ Backplane ]
	Supported link modes:   1000baseKX/Full
	                        10000baseKR/Full
	                        25000baseCR/Full
	                        25000baseKR/Full
	                        25000baseSR/Full
	Supported pause frame use: Symmetric
	Supports auto-negotiation: Yes
	Supported FEC modes: None	 RS	 BASER
	Advertised link modes:  1000baseKX/Full
	                        10000baseKR/Full
	                        25000baseCR/Full
	                        25000baseKR/Full
	                        25000baseSR/Full
	Advertised pause frame use: Symmetric
	Advertised auto-negotiation: Yes
	Advertised FEC modes: None
	Speed: 10000Mb/s
	Duplex: Full
	Auto-negotiation: on
	Port: Direct Attach Copper
	PHYAD: 0
	Transceiver: internal
netlink error: Operation not permitted
	Link detected: yes
```