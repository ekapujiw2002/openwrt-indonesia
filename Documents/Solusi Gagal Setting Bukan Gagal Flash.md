# Solusi Gagal Setting Bukan Gagal Flash

Jika terjadi kegagalan pengaturan atau instalasi suatu paket kadang  menyebabkan router tidak dapat diakses baik halaman administrator (http://192.168.1.1) juga melalui *console*. Kondisi ini dapat diatasi  dengan cara sebagai berikut:
1. Matikan dan nyalakan router
2. Sesaat LED SYS menyala tekan tombol QSS
3. Kini router telah dapat diakses melalui **telnet**
4. Login router dengan **telnet**
5. Ketik perintah: 

		firstboot

6. Ketik perintah:

		/etc/init.d/uhttpd start

7. Masuk kembali ke halaman admin di browser dengan alamat: http://192.168.1.1

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](http://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/solusi-gagal-seting-bukan-gagal-flash/343633129011051/
