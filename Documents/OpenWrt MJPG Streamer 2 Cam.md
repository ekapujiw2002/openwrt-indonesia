# OpenWrt MJPG Streamer 2 Cam

1. Install package berikut:
```bash
	opkg update; opkg install kmod-video-uvc kmod-video-core
	ls /dev/ (Cari nama video0 dan video1)
```

2. Install package berikut:
```bash
	opkg update; opkg install mjpg-streamer
```

3. Edit konfigurasi pada file **/etc/config/mjpg-streamer** menjadi seperti konfigurasi dibawah:
```bash
config mjpg-streamer 'core'
        option yuv '0'
        option enabled '1'
        option fps '20'
        option resolution '1280x720'
        option device '/dev/video0'
        option device2 '/dev/video1'
        option port '8080'
        option port2 '8081'
```
