# Kontrol Perangkat Jarak Jauh Menggunakan Serial2Network Ser2Net

<p align="center">
   <img src="https://scontent.fcgk2-1.fna.fbcdn.net/v/t1.0-9/10153860_620710134718575_1794109675636607625_n.jpg?oh=8cc14c39f43956a81e5438374d894700&oe=5A350CE5">
</p>

Ser2Net berguna untuk kontrol perangkat jarak jauh. Metode ini dapat diterapkan untuk berbagai macam perangkat, baik: server, drone, rocket, missille, sensor, awlr, sismograf, dan lain-lain.

Bagaimana kecantikan arsitekturnya tergantung bagaimana anda meracik dan menghiasnya sehingga secure, safe and sound. Berikut contoh menggunakan perangkat komunikasi **serial ch341**, driver disesuaikan dengan perangkat yg digunakan.

## Instalasi
```bash
root@Openwrt:~# opkg kmod-usb-serial-ch341
root@Openwrt:~# pkg install ser2net
root@Openwrt:~# echo 1234:raw:0:/dev/ttyUSB0:115200 >> /etc/ser2net.conf
```

## Running
```bash
ser2net
```

<p align="center">
   <img src="https://scontent.fcgk2-1.fna.fbcdn.net/v/t1.0-9/1601476_620710624718526_3988268206683154205_n.jpg?oh=c51825d4ee1a886ddf160d90b6bd9075&oe=5A326C08">
</p>

## Akses dengan PuTTY atau sejenisnya:

Akses dengan putty atau sejenisnya:
- Hostname        : IP_VPN
- Connection type : RAW
- Port            : 1234

Selesai...

Kontribusi :
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/kontrol-perangkat-jarak-jauh-menggunakan-serial2network-ser2net/814684408572585/
