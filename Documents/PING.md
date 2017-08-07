# PING

1. Buat file tester di /bin
```bash
root@OpenWrt:~# vi /bin/tester.sh
isinya : tekan i

#!/bin/sh
if ! ping -q -c 3 -W 10 8.8.8.8 > /dev/null; then
(ifup wan) &
fi

simpan : tekan Esc lalu ketik :wq
root@OpenWrt:~#
```

```bash
2. root@OpenWrt:~# touch /bin/tester.sh
root@OpenWrt:~#chmod 755 /bin/tester.sh
root@OpenWrt:~#/etc/init.d/cron stop
root@OpenWrt:~#echo "*/2 * * * * /bin/tester.sh" >> /etc/crontabs/root
root@OpenWrt:~# /etc/init.d/cron enable
root@OpenWrt:~# /etc/init.d/cron start
```

3. Cek di LuCI
