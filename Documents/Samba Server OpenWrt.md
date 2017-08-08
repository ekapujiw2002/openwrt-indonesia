# Samba Server OpenWrt

## Package yang dibutuhkan:
	- luci-app-samba
	- samba36-server
	- ntfs-3g

## Langkah-langkah:
1. Edit **/etc/config/firewall** dengan menambahkan baris sebagai berikut:
```bash
config rule
    option src         lan
    option proto         udp
    option dest_port     137-138
    option target        ACCEPT
 
config rule
    option src         lan
    option proto         tcp
    option dest_port     139
    option target        ACCEPT
 
config rule
    option src         lan
    option proto         tcp
    option dest_port    445
    option target        ACCEPT
```

2. Edit **etc/samba/smb.conf.template** menjadi:
```bash
[global]
    netbios name = |NAME|
    workgroup = |WORKGROUP|
    server string = |DESCRIPTION|
    syslog = 10
    encrypt passwords = true
    passdb backend = smbpasswd
    obey pam restrictions = yes
    socket options = TCP_NODELAY
    unix charset = ISO-8859-1
        local master = yes
    preferred master = yes
    os level = 20
    security = share
    guest account = nobody
    invalid users = root
    smb passwd file = /etc/samba/smbpasswd
```

3. Tambahkan pada file **/etc/config/samba**:
```bash
config 'samba'
    option 'name' 'openwrt'
    option 'description' 'openwrt'
    option 'workgroup' 'WORKGROUP'
 
config 'sambashare'
    option 'read_only' 'no'
    option 'create_mask' '0700'
    option 'dir_mask' '0700'
    option 'name' 'samba'         
    option 'path' '/mnt/sdb2'   <=== Sesuaikan dengan drive yang akan diakses
    option 'guest_ok' 'yes'
```

4. Tambahkan baris berikut pada file **/etc/rc.local**:
```bash
smbd -D
nmbd -D
 
exit 0
```

5. Ketik perintah berikut pada **PuTTY**:
```bash
/etc/init.d/samba enable
/etc/init.d/samba start
```

**NOTE**:
- Jika drive yg akan kita akses berformat "ntfs", maka kita harus menambahkan command berikut pada "putty" agar bisa full akses (baca,tulis, hapus)
		umount /dev/sdx*
		ntfs-3g /dev/sdx* /mnt/sdb*

**KETERANGAN:
x = ganti sesuai dengan terdeteksinya drive kita, misal "sdb","sdc","sdd" dst.
* =  jika partisi drive "ntfs" lebih dari 1, maka lakukan langkah di atas sebanyak jumlah partisi. tanda "*"(bintang) diganti dengan jumlah partisi

Restart router

6. Pada Windows XP/7 masuk ke RUN ketik "cmd" ,lalu ENTER, ketik perintah :
		net use S: \\192.168.1.1\samba

FINISH!!!
Silahkan akses di "COMPUTER(win7)/MY COMPUTER(Windows XP)"

Kontribusi:
- Terima Kasih kepada [Tisaros Obengkumana](https://www.facebook.com/tisaros.obengkumana)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/samba-server-openwrt/373714092669621/
