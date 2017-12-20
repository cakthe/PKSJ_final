### 2.1. Pendahuluan

Cuckoo merupakan sebuah sistem _open source_ otomatis untuk analisis _malware_. Cuckoo digunakan untuk berjalan dan menganalisis _file-file_ secara otomatis, kemudian mengumpulkan hasil analisis lengkap yang menguraikan apa yang dilakukan oleh _malware_ selama berjalan di dalam sistem operasi terisolasi. Cuckoo dapat mengambil hasil dari:

* Jejak yang ditinggalkan semua proses yang ditelurkan oleh _malware_.
* _File_ yang dibuat, dihapus, dan diunduh oleh malware selama eksekusi _malware_.
* _Memory dump_ dari proses-proses _malware_.
* Jejak _network traffic_ dalam format PCAP.
* _Screenshot_ yang diambil selama eksekusi _malware_.
* Keseluruhan _memory dump_ dari mesin.

### 2.2. Instalasi

Dengan _host_ Ubuntu 16.04, paket-paket yang perlu diinstal:
```
$ sudo apt-get install git mongodb libffi-dev libjpeg-dev zlib1g-dev build-essential python-django python python-dev python-pip python-pil python-sqlalchemy python-bson python-dpkt python-jinja2 python-magic python-pymongo python-gridfs python-libvirt python-bottle python-pefile python-chardet tcpdump apparmor-utils autoconf libtool libjansson-dev libmagic-dev libssl-dev swig -y
```

#### 2.2.1. Yara

```
$ wget https://github.com/plusvic/yara/archive/v3.4.0.tar.gz -O yara-3.4.0.tar.gz
$ tar -zxf yara-3.4.0.tar.gz
$ cd yara-3.4.0
$ ./bootstrap.sh
$ ./configure --with-crypto --enable-cuckoo --enable-magic
$ make
$ sudo make install
```

Kemudian _build_ dan _install_ ekstensi **yara-python**:
```
$ cd yara-python
$ python setup.py build
$ sudo python setup.py install
```

#### 2.2.2. Pydeep

Untuk instalasi **pydeep**, perlu juga _install_ **ssdeep 2.8+**, maka:
```
$ wget http://sourceforge.net/projects/ssdeep/files/ssdeep-2.13/ssdeep-2.13.tar.gz/download -O ssdeep-2.13.tar.gz
$ tar -zxf ssdeep-2.13.tar.gz
$ cd ssdeep-2.13
$ ./configure
$ make
$ sudo make install
```

Barulah instalasi **pydeep**:
```
$ pip install pydeep
```

#### 2.2.3. Volatility

Untuk instalasi **volatility**, sebelumnya perlu:
```
$ pip install openpyxl
$ pip install ujson
$ pip install pycrypto
$ pip install distorm3
$ pip install pytz 
```

Kemudian:
```
$ git clone https://github.com/volatilityfoundation/volatility.git
$ cd volatility
$ python setup.py build
$ python setup.py install
```

#### 2.2.4. VirtualBox

Untuk virtualisasinya, di sini digunakan **VirtualBox**. Maka perlu juga diinstall dengan:
```
$ sudo apt-get install vitualbox
```

#### 2.2.5. Cuckoo

```
$ git clone git://github.com/cuckoosandbox/cuckoo.git
```

### 2.3. Konfigurasi

#### 2.3.1. Tcpdump

Tcpdump normalnya membutuhkan hak sebagai root. Tapi karena Cuckoo tidak berjalan sebagai root, maka perlu dikonfigurasi:
```
$ sudo setcap cap_net_raw,cap_net_admin=eip /usr/sbin/tcpdump
```

#### 2.3.2. VirtualBox

#### 2.3.3. Cuckoo


### 2.4. Skenario

### 2.5. Hasil
