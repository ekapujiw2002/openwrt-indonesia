# OpenWrt Modem ZTE K3806Z

## Install Package:
```bash
   opkg update; opkg install chat comgt kmod-nls-base kmod-usb-core kmod-usb-ohci kmod-usb-serial-option kmod-usb-serial-wwan kmod-usb-serial 
kmod-usb-uhci kmod-usb2 libpthread librt libusb-1.0 luci-proto-3g  usb-modeswitch luci kmod-usb-acm kmod-usb-atm
```

## Buat Interface baru via LuCI biar mudah:

Sesuaikan saja, **Modem ZTE K3806Z** terdeteksi sebagai /dev/ttyACM0, /dev/ttyACM1, /dev/ttyACM2, dan yang bisa digunakan untuk koneksi data adalah 
**/dev/ttyACM0**

Kontribusi:
- Terima Kasih kepada [Dian Ariyanto](https://www.facebook.com/sompaksompil)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/pengaturan-modem-zte-k3806z-devttyacm0/1111815058859517/
