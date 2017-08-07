# SMS Gateway Menggunakan Gnokii

## INSTALL PACKAGE SMS GATEWAY
      root@OpenWrt:~# opkg install gnokii bluez-libs libpcsclite kmod-usb-core kmod-usb-serial-option usb-modeswitch usb-modeswitch-data
## SETTING SMS GATEWAY
      root@OpenWrt:~# ls /dev/ttyUSB*
      /dev/ttyUSB0 #ANE GUNAIN UNTUK INTENET ALIAS MODEM
      /dev/ttyUSB1 #ANE PAKEK INI UNTUK SMS SMSGATEWAY
      
      root@OpenWrt:~# vim /etc/gnokiirc
      [global]
      model = AT
      port = /dev/ttyUSB1 connection = serial
      
      root@OpenWrt:~# vim /root/.gnokiirc
      [global]
      model = AT
      port = /dev/ttyUSB1 connection = serial
      
## CEK SETTING SMS GATEWAY
    root@OpenWrt:~# gnokii --identify
    GNOKII Version 0.6.21
    IMEI         : 358093021456721
    Manufacturer : QUALCOMM INCORPORATED
    Model        : C-180
    Product name : C-180
    Revision     : 120016_062_001
    
## TES KIRIM SMS
    echo "TES SMS GATEWAY DENGAN GNOKII" | tr '+' ' ' | gnokii --sendsms +6288217134491
    #ane pakek "tr" cz q buat konversi dari simbol "+" menjadi {spasi}, bakal berguna jika digunain di web dengan method GET, btw dihilangkan juga gpp
    
## LIHAT SMS MASUK
    gnokii --getsms SM 0 #LIHAT SMS DENGAN ID 0
    gnokii --getsms SM 0 end #LIHAT SEMUA SMS
    
## HAPUS SMS MASUK
    gnokii --deletesms SM 0 #HAPUS SMS DENGAN ID 0
    gnokii --deletesms SM 0 end #HAPUS SEMUA SMS

Kontribusi :
- Terima Kasih kepada [Agustian Romy Ariansyah]https://www.facebook.com/agustianra
- Terima Kasih kepada [OpenWrt Indonesia]http://www.facebook.com/groups/openwrt

Referensi :
- https://www.facebook.com/notes/openwrt-indonesia/share-sms-gateway-dengan-menggunakan-gnokii/528197040554658/
