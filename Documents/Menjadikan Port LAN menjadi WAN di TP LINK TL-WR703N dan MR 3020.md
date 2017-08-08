# Menjadikan Port LAN menjadi WAN di TP LINK TL-WR703N & MR 3020

**config 'interface' 'loopback'**
```bash
	option 'ifname' 'lo'
	option 'proto' 'static'
	option 'ipaddr' '127.0.0.1' option 'netmask' '255.0.0.0'
```

**config 'interface' 'lan'**
```bash
	option 'ifname' 'wlan0'
	#option 'type' 'bridge'
	option 'proto' 'static'
	option 'ipaddr' '192.168.1.1' option 'netmask' '255.255.255.0'
```

**config 'interface' 'wan1'**
```bash
	option 'ifname' 'ppp0'
	option 'device' '/dev/ttyUSB0'
	option 'service' 'evdo'
	option 'proto' '3g'
	option 'apn' 'smart'
	option 'username' 'smart' option 'password' 'smart'
```

**config 'interface' 'wan2'**
```bash
	option 'ifname' 'eth0'
	option 'type' 'dhcp'
	#option 'proto' 'static'
	#option 'ipaddr' '192.168.1.1' #option 'netmask' '255.255.255.0'
```

**/etc/config/firewall**
**config 'zone'**
```bash
	option 'name' 'internet'
	option 'network' 'wan1 wan2'
	option 'input' 'REJECT'
	option 'forward' 'REJECT'
	option 'output' 'ACCEPT' option 'masq' '1'
```

**config 'forwarding'**
```bash
	option 'src' 'local' option 'dest' 'internet'
```

**config 'zone'**
```bash
	option 'name' 'local'
	option 'network' 'lan'
	option 'input' 'ACCEPT'
	option 'forward' 'REJECT' option 'output' 'ACCEPT'
```

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/menjadikan-port-lan-menjadi-wan-di-tp-link-tl-wr703n-mr-3020/344479875593043/
