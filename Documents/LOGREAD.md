# LOGREAD

Kemarin waktu masih pake **LuCI** *troubleshoot* nya enak, tinggal masuk ke *kernel log* / *system log*. Nah untuk mode *text/cli* gimana yah ?
Setelah iseng iseng tanya tanya mbah **Google**, akhirnya nemu juga nih. Kalo di **Linux** sih pake command ini:

```bash
		tail -f /var/log/message
```

Nah kalau di **OpenWrt** kita pakai command:
```bash
		logread
```
