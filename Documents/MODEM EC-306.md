# MODEM EC-306

**/etc/modules.d/60-usb-serial gak usah di edit gan**.

Isinya dihapus saja. lalu coba colok *ce210* nya, liat detect atau tidak? untuk *ec-306* agan bisa bikin kayak gini:

```bash
		vi /etc/usb_modeswitch.d/12d1:1505
```

Isi pake ini:

```bash
########################################################
# Huawei EC156, EC306
DefaultVendor= 0x12d1
DefaultProduct=0×1505
TargetVendor= 0x12d1
TargetProductList=”140b,1506?
MessageContent=”55534243123456780000000000000011062000000100000000000000000000?
CheckSuccess=20
########################################################
```

Kemudian *save* : Tekan **Esc** kemudian ketik **:wq** kemudian **Enter**
Trus agan coba colok lagi modem **ec-306** nya. Moga moga bisa

Kontribusi:
- Terima Kasih kepada [Cindy Wijaya](https://www.facebook.com/openwrtindonesia)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/modem-ec-306/343640609010303/
