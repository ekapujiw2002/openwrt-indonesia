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
4. Edit konfigurasi pada file **/etc/init.d/mjpg-streamer** menjadi seperti konfigurasi dibawah:
```bash
#!/bin/sh /etc/rc.common
# Copyright (C) 2009-2012 OpenWrt.org

START=50

SERVICE_DAEMONIZE=1
SERVICE_WRITE_PID=1

PROG=/usr/bin/mjpg_streamer

error() {
        echo "${initscript}:" "$@" 1>&2
}

section_enabled() {
        config_get_bool enabled "$1" 'enabled' 0
        [ $enabled -gt 0 ]
}

start_instance() {
        local s="$1"
        local auth=""

        section_enabled "$s" || return 1


        config_get device "$s" 'device'
        config_get resolution "$s" 'resolution'
        config_get fps "$s" 'fps'
        config_get yuv "$s" 'yuv' 0
        config_get port "$s" 'port'
        config_get www "$s" 'www' "/usr/lib/mjpg-streamer/www"
        config_get username "$s" 'username'
        config_get password "$s" 'password'

        [ $yuv = "1" ] && yuv="-y" || yuv=""

        [ -c "$device" ] || {
                error "device '$device' does not exist"
                return 1
        }

        [ -n "$username" -a -n "$password" ] && {
                auth="--credentials $username:$password"
        }

        service_start /usr/bin/mjpg_streamer --input "input_uvc.so $yuv --device $device --fps $fps --resolution $resolution" --output "output_http.so 
--www $www --port $port $auth"
}

stop_instance() {
        local s="$1"

        section_enabled "$s" || return 1

        service_stop /usr/bin/mjpg_streamer
}

start() {
        config_load 'mjpg-streamer'
        config_foreach start_instance 'mjpg-streamer'
}

stop() {
        config_load 'mjpg-streamer'
        config_foreach stop_instance 'mjpg-streamer'
}
```
5. Buat file **mjpg-streamer2** didalam folder **/etc/init.d/** dengan config berikut:
```bash
#!/bin/sh /etc/rc.common
# Copyright (C) 2009-2012 OpenWrt.org

START=50

SSD=start-stop-daemon
NAME=mjpg_streamer
PIDF=/var/run/$NAME.2.pid
PROG=/usr/bin/$NAME

SERVICE_DAEMONIZE=1
SERVICE_WRITE_PID=1


error() {
        echo "${initscript}:" "$@" 1>&2
}

section_enabled() {
        config_get_bool enabled "$1" 'enabled' 0
        [ $enabled -gt 0 ]
}

start_instance() {
        local s="$1"
        local auth=""

        section_enabled "$s" || return 1


        config_get device "$s" 'device2'
        config_get resolution "$s" 'resolution'
        config_get fps "$s" 'fps'
        config_get yuv "$s" 'yuv' 0
        config_get port "$s" 'port2'
        config_get www "$s" 'www' "/usr/lib/mjpg-streamer/www"
        config_get username "$s" 'username'
        config_get password "$s" 'password'


        [ $yuv = "1" ] && yuv="-y" || yuv=""

        [ -c "$device" ] || {
                error "device '$device' does not exist"
                return 1
        }

        [ -n "$username" -a -n "$password" ] && {
                auth="--credentials $username:$password"
        }

        service_start /usr/bin/mjpg_streamer --input "input_uvc.so $yuv --device $device --fps $fps --resolution $resolution" --output "output_http.so 
--www $www --port $port $auth -p $PIDF"
}

stop_instance() {
        local s="$1"

        section_enabled "$s" || return 1

        service_stop /usr/bin/mjpg_streamer
}

start() {
        config_load 'mjpg-streamer'
        config_foreach start_instance 'mjpg-streamer'
[ $enabled -gt 0 -a -c $device ] && sleep 3 && $SSD -S -m -p $PIDF -q -x $PROG --input "input_uvc.so --device $device --fps $fps --resolution 
$resolution" --output "output_http.so --port $port"
}

stop() {
        config_load 'mjpg-streamer'
        config_foreach stop_instance 'mjpg-streamer'
}
```

6. Jalankan **mjpg-streamer** dengan perintah berikut:
```bash
mjpg_streamer -i "input_uvc.so -d /dev/video0 -r 1280x720" -o "output_http.so -p 8080 -w /www/webcam1"&mjpg_streamer -i "input_uvc.so -d /dev/video1 -r 
640x480" -o "output_http.so -p 8081 -w /www/webcam2"&
```

Kontribusi:
- Terima Kasih kepada [Nova Si Kalem](https://www.facebook.com/ahteuing)
- Terima Kasih kepada [OpenWrt Indonesia](http://www.facebook.com/groups/openwrt)

Referensi:
- https://lookaside.fbsbx.com/file/mjpg%20streamer%202%20cam.txt?token=AWymULfMyG97tVvPNL5I49Oc_ttUTKPQFqWdqMVRSAHDH7ZWEDFke3J6WhPnYGdazC8l3tOFYPYYS_4eJ-HBTFEPJoU4_wt_9qB_i7LfvDlMDfx2DiqDm3bPZKUtp_gu-lP9wo0adXDAATbssgXSI8uYqzTGlRnRBvsjpdT6-s-Z6w
