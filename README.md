#linux-rpl

##**RPL: IPv6 Routing Protocol for Low-Power and Lossy Networks for Linux**

### rpl-userspace-tools
Userspace tools to setup, manage, list and check RPL configurations

https://github.com/joaopedrotaveira/rpl-userspace-tools

### rpl-kernel
Kernel patches

* Mainline
	* v3.10
	* v3.11
	* v3.12
* raspberrypi 3.10.y

https://github.com/joaopedrotaveira/linux-rpl

## Using RPL

### Setting up root
```
# in root mode, kernel will use iface addr as dodag id
$ sudo ip addr add 2001:aaaa:beef:c0fe::1/64 dev lowpan0

# setup iface to act as dodag root
$ sudo sysctl -w net.ipv6.conf.lowpan0.rpl_dodag_root=1

# enable rpl on iface
$ sudo sysctl -w net.ipv6.conf.lowpan0.rpl_enabled=1
```

### Setting up RPL router
```
# enable without rpl-userspace-tools
$ sudo sysctl -w net.ipv6.conf.lowpan0.rpl_enabled=1
```
```
# enable with rpl-userspace-tools
$ sudo rpl-ctl enable lowpan0
```

### Disable IPv6 Privacy Extensions
RPL module announces all global IPv6 addresses of RPL enabled iface. It might not be desired to announce 2 or 3 addresses of each node to DAG.

To disable IPv6 Privacy Extensions:
```
$ sudo sysctl -w net.ipv6.conf.all.use_tempaddr = 0
$ sudo sysctl -w net.ipv6.conf.default.use_tempaddr = 0
```