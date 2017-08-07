# OpenWrt Parsing Query String Lua

Untuk yang bertanya untuk apa si *parsing* ini?, misal anda ingin memerintahkan sesuatu command di router tanpa masuk ke PuTTY (CLI), dengan *parsing* 
ini dapat mengontrol  perintang *cli* dengan *websocket*. 

Saya beri contoh parsing: http://192.168.1.1/parsing.lua?saklar1=on&saklar2=off

Maka router memerintahkan untuk saklar 1 nyala dan saklar 2 mati, di sini saya mencoba membuat contoh *parsing* dengan lua *script*. untuk yang bisa 
mengembangkan nya boleh tulis di comment. ok kita mulai contoh script nya:

1. Buat *file* baru dengan nama **parsing.lua** didalam *directory* /www/cgi-bin/
2. Isi dari file **parsing.lua** adalah sebagai berikut:
```lua
#!/usr/bin/env lua
print ("Content-type: Text/html\n")
local info = os.getenv("QUERY_STRING")
local params = {}
local echo = {}
for name, value in string.gmatch(info .. '&', '(.-)%=(.-)%&') do
        value = string.gsub(value , '%+', ' ')
        value = string.gsub(value , '%%(%x%x)', function(dpc)
                return string.char(tonumber(dpc,16))
                end )
        params[name] = value
        value = string.gsub(value, "%&", "&amp;")
        value = string.gsub(value, "%<", "&lt;")
        value = string.gsub(value, '%"', "&quot;")
        echo[name] = value
        end
pagetop = [[
<html>
<head>
<title>contoh parsing lua</title>
</head>
<body>
<form>input data :
<br>
<input name=saklar1 value='on'><br>
<input name=saklar2 value='on'><br>
<input name=saklar3 value='on'><br>
<input name=saklar4 value='on'><br>
<input name=saklar5 value='on'><br>
<input name=saklar6 value='on'><br>
<input name=saklar7 value='on'><br>
<input name=saklar8 value='on'><br>
<br>
<input type=submit value="kirim"></form>
Result:
<br>
]]
print (pagetop)
        if params["saklar1"] == "on" then
                print ("OK saklar1 status NYALA<br>")
        elseif params["saklar1"] == "off" then
                print ("OK saklar1 status MATI<br>")
        end
	if params["saklar2"] == "on" then
                print ("OK saklar2 status NYALA<br>")
        elseif params["saklar2"] == "off" then
                print ("OK saklar2 status MATI<br>")
        end
	if params["saklar3"] == "on" then
                print ("OK saklar3 status NYALA<br>")
        elseif params["saklar3"] == "off" then
                print ("OK saklar3 status MATI<br>")
        end
	if params["saklar4"] == "on" then
                print ("OK saklar4 status NYALA<br>")
        elseif params["saklar4"] == "off" then
                print ("OK saklar4 status MATI<br>")
        end
	if params["saklar5"] == "on" then
                print ("OK saklar5 status NYALA<br>")
        elseif params["saklar5"] == "off" then
                print ("OK saklar5 status MATI<br>")
        end
	if params["saklar6"] == "on" then
                print ("OK saklar6 status NYALA<br>")
        elseif params["saklar6"] == "off" then
                print ("OK saklar6 status MATI<br>")
        end
	if params["saklar7"] == "on" then
                print ("OK saklar7 status NYALA<br>")
        elseif params["saklar7"] == "off" then
                print ("OK saklar7 status MATI<br>")
        end
	if params["saklar8"] == "on" then
                print ("OK saklar8 status NYALA<br>")
        elseif params["saklar8"] == "off" then
                print ("OK saklar8 status MATI<br>")
        end

pagebase = [[
</body>
</html>
]]
print (pagebase)
```
3. Berikan permission pada file **parsing.lua** dengan command:
```bash
		chmod 0755 /www/cgi-bin/parsing.lua
```
4. Coba akses di browser anda: http://192.168.1.1/cgi-bin/parsing.lua

Selesai & Semoga bermanfaat...

Kontribusi:
- Terima Kasih kepada [Friyadhi Biermann](https://www.facebook.com/friyadhi.biermann)
- Terima Kasih kepada [OpenWrt Indonesia](https://www.facebook.com/groups/openwrt)

Referensi:
- https://www.facebook.com/notes/openwrt-indonesia/parsing-querysrting-lua/1472516556122697/
