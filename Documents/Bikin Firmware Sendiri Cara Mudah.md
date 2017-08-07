# Bikin Firmware Sendiri Cara Mudah

## Membuat full backup image openwrt dari Router Aktif (cloning image)
Ketika kita capek install berbagai *package* pada router **OpenWrt** dan router sudah  *ready online*. Namun ditengah-tengah ada gagal *setting*, maka 
kita harus flash dari awal, atau *reset* menggunakan *command* **firstboot**.

Adakah cara lain untuk menyelamatkan *image* yang telah terinstall berbagai *package* yang dibutuhkan, seperti LuCI Web Interface + Driver USB Modem dan 
lain. Awalnya saya tidak yakin menggunakan cara ini, masih bimbang antara router jadi *brick* atau *on* sesuai harapan

**OpenWrt** menyimpan *firmware* pada **mtd5** atau tempat menyimpan *image yang kita *flash* ke router ternyata di **mtd5**. Setelah di install 
berbagai *package* juga dimasukkan ke **mtd5**.

## Langkah *backup*
1. Login router seperti biasa menggunaka protokol SSH
2. Pastikan *firmware* tersimpan pada **mtd** berapa dengan command:

		cat /proc/mtd
		
3. Backup dengan command:

		cat /dev/mtdX > /tmp/factory.bin
		mtdX disesuaikan dengan mtd yang terdetek pada router yang anda gunakan 
Perintah diatas akan membuat file baru dengan nama **factory.bin** pada folder **/tmp**. Simpan baik baik *file* tersebut. Untuk *flash* kembali ke router, cukup *flash* sesuai *flash image* standar saja, bisa *upgrade* dari *Web Interface* atau menggunakan WinSCP untuk mengupload image ke folder /tmp dan dieksekusi dengan command:

		cd /tmp && mtd -e firmware -r write factory.bin firmware

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/bikin-firmware-sendiri-cara-mudah/343768642330833/
- http://inranrumani.blogspot.co.id/2011/10/membuat-full-backup-image-openwrt-dari.html
- https://wiki.openwrt.org/doc/techref/mtd
- https://wiki.openwrt.org/doc/howto/generic.backup
