# Project Si Jabrick

## Module yang digunakan:
- Voice Recognition V3 http://www.elechouse.com/elechouse/index.php?main_page=product_info&cPath=&products_id=2254
- USB SoundCard + Speaker
- USB TO TTL

## Langkah-langkah:
1. Konekkan **module** denga **USB TO TTL**:

| USB TO TTL    | MODULE        |
|:-------------:|:-------------:|
|GND	        	| GND		        |
|RX		          | TX		        |
|TX		          | RX		        |
|VCC 		        | VCC		        |

2. Install package:
```bash
    python
    pyserial
    kmod-sound-core
    kmod-usb-audio
    alsa-utils
    madplay
```

3. Download script dan config : https://app.box.com/s/09x1o8bv3rkio2jiuyl8bt31nwbsccv5
4. Upload file **jabrik** ke **/usr/bin** dan **jabrik.conf** ke folder **/etc**
5. Setting permission **chmod 755 /usr/bin/jabrik**
6. Sesuaikan file **jabrik.conf**:
	- bautrate '9600'
	- device '/dev/ttyUSB3'
	- untuk bautrate saya lupa waktu baru dapat defaultnya berapa jadi coba coba saja jika 9600 gagal ganti 2400,4800,19200,38400 untuk device sesuaikan dengan **USB TO TTL** 
7. Cobalah dengan ketik **jabrik clear**. jika Clr OK berarti sambungan sudah bagus.
8. Buka lagi file **jabrik.conf** edit dengan mengikuti contoh yang ada dan sedikit keterangn mudah-mudahan bisa dipahami wkwkwk
9. Jalankan jabrik dengan ketik **jabrik** run silahkan kreasikan sesuai keinginan dengan edit file confignya

**NOTE**:
- Untuk memulai voice recognition harus diisi suara terlebih dahulu dengan perintah jabrik sigtrain [index] text
  contoh **jabrik sigtrain 0 JABRIK**
  
  0 disini adalah indek penyimpanan dimulai dari 0 - 80

- jika butuh info lebih mendalam coba lihat datasheet modul **voice regocnition** karena saya sendiri baru memahami modul tersebut wkwkwk

Video si Jabrik: https://www.youtube.com/watch?v=5absoDlwUF0

Kontribusi: 
- Terima Kasih kepada [Mikodemos Ragil](https://www.facebook.com/mikodemos.ragil)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/project-si-jabrik/972425219465169/
