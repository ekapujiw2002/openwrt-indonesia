# Game Online Mode NAT

Buat main *game online* tapi *NAT Mode* : STRICT (xbox360 & PS3)

Install *package*:
```bash
	opkg update; opkg install miniupnp
```

Buat *auto* dan *trigger* pada saat *boot*:
```bash
	root@OpenWrt# /etc/init.d/miniupnpd enable
	root@OpenWrt# /etc/init.d/miniupnpd start
```

*NAT* type nya langsung *OPEN*:

**WARNING**: Hanya aktifkan jika main *game online* saja, kalo untuk *browsing deactive* lagi soalnya semua *port* otomatis terbuka... *cheers*

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/game-online-mode-nat/343639545677076/
