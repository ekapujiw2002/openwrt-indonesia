# Ganti Jaringan 2G - 3G

Package: **microcom** atau yang sejenis: **minicom**, dan sebagainya.

1. Panggil *modem* dengan cara sebagai berikut:

		microcom -D/dev/ttyUSB2

2. Ketika keluar angka gak jelas *switch modem* dengan cara copas:

		AT^SYSCFG=13,1,3FFFFFFF,1,2 Kemudian tekan ENTER

3. Buka LuCI, Klik Network->Interface *reconnect this interface* dibagian WAN
4. Lihat sampai dapat IP atau kalau gak liat di *modem* biasanya nyala warna hijau
5. Setelah konek atau terhubung copas:

		AT^SYSCFG=14,2,3FFFFFFF,1,2 Kemudian tekan ENTER


Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](http://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](http://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/ganti-jaringan-2g-3g/343633652344332/
