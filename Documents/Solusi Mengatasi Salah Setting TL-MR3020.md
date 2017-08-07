# Solusi Mengatasi Salah Setting TL-MR3020

1. Matikan *router*, cabut kabel *power*
2. Setting IP PC/Labtop
		* Address : 192.168.1.69
		* Netmask : 255.255.255.0
		* Gateway : 192.168.1.1
3. Nyalakan *router* colokkan kabel *power*
4. Pada saat menyala, perhatikan *LED* yang didekat tombol *reset*:
		* Menyala
		* Berkedip sekali
		* Menyala agak lama
5. Pada saat *LED* mulai berkedip lagi, tekan tombol *reset* maka *LED* akan berkedip dengan cepat, bila **tidak** berarti **gagal** ulangi dari nomor 
3.
6. Buka aplikasi **PuTTY** dengan hostname **192.168.1.1** dengan *Connection port* **telnet**. Semestinya sudah tampil OpenWrt, bila tidak ulangi dari 
nomor 3.
7. Bila sudah berhasil akses OpenWrt dengan **telnet** ketik perintah berikut:
		mount_root
		firstboot
8. reboot

Kontribusi:
- Terima Kasih kepada (Gandhi Wibowo)[https://www.facebook.com/gandhiw3]
- Terima Kasih kepada (OpenWrt Indonesia)[https://www.facebook.com/groups/openwrt]

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/solusi-mengatasi-salah-setting-mr-3020/1469322763108743/
