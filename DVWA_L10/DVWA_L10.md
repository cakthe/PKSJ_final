# DVWA | Lesson 5
## Konfigurasi

### { Upload PHP Backdoor Payload }

pada lesson 10, kami menggunakan metasploid dan backtrack.

- pertama-tama agar backtrack dan metasploit mendapat IP, buka vm -> klik kanan -> setting -> network -> pilih bridge adapter

![alt text](./backtrack.PNG)

![alt text](./metasploit.PNG)

Alamat target DVWA (metasploitable) 
`http://10.151.34.170`

Alamat penyerang (backtrack)
`http://10.151.34.160`


## Skenario

- start metasploit dan backtrack yang sudah dikonfigurasi

- buka DVWA pada firefox yang ada di backtrack
- login dengan user : admin dan password : password
![alt text](./16.PNG)
- kali ini kita akan mencoba mengganti password dengan CSRF
- masuk ke halaman CSRF
![alt text](./1.PNG)
- ganti password sesuai yang diinginkan
- kami menggunakan asd123 sebagai password baru
![alt text](./2.PNG)
- password berhasil diubah
![alt text](./3.PNG)
- copy url yang ada
![alt text](./4.PNG)
- buka notepad, dan paste url yang sudah dicopy tadi
![alt text](./5.PNG)
- coba logout dvwa
![alt text](./6.PNG)
- coba login kembali menggunakan password yang sudah diubah
- kami menggunakan asd123 sebagai password baru
![alt text](./7.PNG)
- set DVWA security menjadi low
![alt text](./8.PNG)
- buka halaman xss reflected
- submit cookies : 
    `<script>alert(document.cookie)</script>`
![alt text](./9.PNG)
- cookies berhasil disubmit
![alt text](./10.PNG)
- sekarang copy hasil pop up yang ada
![alt text](./11.PNG)
- buka notepad lagi, dan paste 
![alt text](./12.PNG)
- sekarang  buatlah script baru dengan ketentuan sebagai berikut
![alt text](./13.PNG)
- copy dan paste script baru ke dalam terminal
- coba ganti lagi password yang ada
- jangan lupa tambahkan :
    `| grep "Password Changed" | tee curl.txt`
![alt text](./14.PNG)






## Hasil
password berhasil diubah dengan menggunakan tee curl.txt
![alt text](./15.PNG)
![alt text](./16.PNG)
![alt text](./17.PNG)