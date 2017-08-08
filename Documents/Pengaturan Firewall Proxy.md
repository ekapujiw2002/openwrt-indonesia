# Pengaturan Firewall Proxy

## The rule below redirects all outgoing HTTP traffic from lan through a proxy server listening at port 3128 on the router itself.
```bash
config redirect
	option src lan
	option proto tcp
	option src_dport 80
	option dest_port 3128
```

## The following rule redirects all outgoing HTTP traffic from lan through an external proxy at 192.168.1.100 listening on port 3128.
```bash
config redirect
	option src lan
	option proto tcp
	option src_ip !192.168.1.100
	option src_dport 80
	option dest_ip 192.168.1.100
	option dest_port 3128
	option target DNAT
 
config redirect
	option dest lan
	option proto tcp
	option src_dip 192.168.1.1
	option dest_ip 192.168.1.100
	option dest_port 3128 option target SNAT
```

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/pengaturan-firewall-proxy/343637139010650/
- http://wiki.openwrt.org/doc/uci/firewall
