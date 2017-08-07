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
		- mtdX disesuaikan dengan mtd yang terdetek pada router yang anda gunakan 

