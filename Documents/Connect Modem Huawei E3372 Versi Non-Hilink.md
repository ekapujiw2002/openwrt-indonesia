# Connect Modem Huawei E3372 Versi Non-Hilink

**NOTE**:
1. Sebelum melakukan settingan jangan colok modem dulu supaya bisa setting firewall
2. Di *interface* memang terlihat **unsupported** tapi sudah bisa konek otomatis

## Langkah-langkah:
1. Install package dengan perintah berikut:
```bash
opkg update; opkg install comgt-ncm kmod-usb-net kmod-usb-net-cdc-ncm kmod-usb-net-huawei-cdc-ncm kmod-usb-wdm;
```

2. Tambahkan konfigurasi berikut tanpa menghapus konfigurasi yang sudah ada pada file **/etc/config/network**:
```bash
	vi /etc/config/network
```
Isi dengan:
```bash
config interface 'wan'
    option proto 'ncm'
    option device '/dev/cdc-wdm0'
    option apn 'indosat3g'
    option pincode '*99#'
    option service 'ncm'
    option delay '10'
```

3. Ubah Interface WAN di Firewall Settings menjadi WAN

Kontibusi:
- Terima Kasih kepada [Rendy Pahlevy](https://www.facebook.com/rendy.pahlevy)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/connect-modem-huawei-e3372-versi-non-hilink/1197662313608124/

