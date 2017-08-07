# OpenWrt Gmail Server
Sebenarnya saya cuman ngelanjutin dari sini :http://openwrtindonesia.blogspot.co.id/2013/09/openwrt-mengirim-email-dengan-openwrt.html Cuman kan emailnya ga terhubung ke gmail. hmm gimana ya OpenWrt ini supaya bisa sinkron dengan gmail?.

Googling ternyata bisa pakai **ssmtp** dengan **mutt**. Supaya ga hilang, saya buat doc gimana caranya agar openwrt bisa konek ke server gmail. Gunanya buat apa?
- Kirim file gerakan/motion ke gmail
- Kirim email ke pengguna lain
- Kirim file attachment dari OpenWrt ke email pengguna lain

## Langkah-Langkah:

1. Install package-package berikut:
```bash
	opkg update; opkg install ssmtp mutt
```
	ChaosCalmer tidak tersedia package **mutt**. bisa diambil dari package BarrierBreaker atau bisa juga dicompile sendiri.
2. Konfigurasi **mutt**:
```bash
	nano /root/.muttrc 
```
	Isi dengan konfigurasi berikut:
```bash
set imap_user = 'emailgmailkamu'
set imap_pass = 'passwordgmailkamu'
set folder = imaps://imap.gmail.com/
set spoolfile = '+INBOX'
set postponed ='+[Google Mail]/Drafts'
set record = "+[Gmail]/Sent Mail"
set editor=/usr/bin/nano
set move = no 
set imap_keepalive = 900
bind editor <space> noop
  macro index,pager y "<save-message>=[Gmail]/All Mail<enter><enter>" "Archive"
  macro index,pager d "<save-message>=[Gmail]/Trash<enter><enter>" "Trash"
  macro index gi "<change-folder>=INBOX<enter>" "Go to inbox"
  macro index ga "<change-folder>=[Gmail]/All Mail<enter>" "Go to all mail"
  macro index gs "<change-folder>=[Gmail]/Sent Mail<enter>" "Go to sent Mail"
  macro index gd "<change-folder>=[Gmail]/Drafts<enter>" "Go to all draf"
```
	Jangan lupa di save dengan command, **Ctrl + X** kemudian tekan **Y** kemudian tekan **Enter**

3. Konfigurasi **ssmtp**:
```bash
	nano /etc/ssmtp/ssmtp.conf
```
	Isi dengan konfigurasi berikut:
```bash
root=emailkamu
mailhub=smtp.gmail.com:465
AuthUser=emailkamu
AuthPass=passwordemailkamu
UseTLS=YES
FromLineOverride=YES
```
        Jangan lupa di save dengan command, **Ctrl + X** kemudian tekan **Y** kemudian tekan **Enter**
4. Konfigurasi **revaliases**:
```bash
	nano /etc/ssmtp/revaliases
```
	Tambahkan konfigurasi berikut pada baris terakhir:
```bash
	root:emailkamu@gmail.com:smtp.gmail.com:465
```

Selesai...
Dicoba dengan mengetikkan **mutt**. Always Accept certificatenya ya.

Untuk pindah label dari inbox ke all mail dengan cara ketik ga, pindah ke draft ketik gd dan lain sebagainya. Shortcutnya bisa ditambah/custom di file 
konfigurasi .muttrc

Untuk mail server yang lain belum dicoba, sepertinya cara kerjanya sama hehe. Tinggal kondisikan alamat dan port ssmptnya. Selamat mencoba, sekian dan 
terima kasih.

Kontribusi:
- Terima Kasih kepada [Andika Trisna Adhi](https://www.facebook.com/GLadIatorV12.UNzip)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/openwrtgmail-server/1446985745342445/
