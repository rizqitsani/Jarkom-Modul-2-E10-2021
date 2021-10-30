# Jarkom-Modul-1-E10-2021

### Kelompok E10

| **No** | **Nama** | **NRP** | 
| ------------- | ------------- | --------- |
| 1 | Muhammad Rizqi Tsani  | 05111940000045 | 
| 2 | Dicksen Alfersius Novian | 05111940000076 |
| 3 | Bill Harit Yafi | 05111940000114 |

## Script

- Foosha
    
    ```python
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.34.0.0/16
    cat /etc/resolv.conf
    ```
    
- Loguetown
    
    ```python
    echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get update
    apt-get install lynx -y
    apt-get install nano -y
    echo nameserver 10.34.2.2 > /etc/resolv.conf
    echo nameserver 10.34.2.3 >> /etc/resolv.conf
    ```
    
- Alabasta
    
    ```python
    echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get install nano -y
    ```
    
- EniesLobby
    
    ```python
    echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get update
    apt-get install bind9 -y
    apt-get install nano -y
    
    mkdir /etc/bind/kaizoku
    
    cp named.conf.local /etc/bind/named.conf.local
    cp franky.e10.com /etc/bind/kaizoku/franky.e10.com
    cp 2.34.10.in-addr.arpa /etc/bind/kaizoku/2.34.10.in-addr.arpa
    
    service bind9 restart
    ```
    
- Water7
    
    ```python
    echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get update
    apt-get install bind9 -y
    apt-get install nano -y
    apt-get install apache2 -y
    apt-get install php -y
    apt-get install libapache2-mod-php7.0
    
    mkdir /etc/bind/sunnygo
    
    cp frannky.e10.com /etc/bind/named.conf.local
    cp mecha.franky.e10.com /etc/bind/sunnygo/mecha.franky.e10.com
    
    service bind9 restart
    service apache2 restart
    ```
    
- Skypie
    
    ```python
    echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get install nano -y
    apt-get install bind9 -y
    apt-get install apache2 -y
    apt-get install php -y
    apt-get install libapache2-mod-php7.0
    
    service apache2 start
    htpasswd -b -c /etc/apache2/.htpasswd luffy onepiece
    cp webserver/franky.e10.com.conf /etc/apache2/sites-available
    cp webserver/super.franky.e10.com.conf /etc/apache2/sites-available
    cp webserver/general.mecha.e10.com-15000.conf /etc/apache2/sites-available/general.mecha.franky.e10.com-15000.conf
    cp webserver/general.mecha.e10.com-15500.conf /etc/apache2/sites-available/general.mecha.franky.e10.com-15500.conf
    a2ensite franky.e10.com
    a2ensite super.franky.e10.com
    a2ensite general.mecha.franky.e10.com-15000.conf
    a2ensite general.mecha.franky.e10.com-15500.conf
    service apache2 restart
    cp -r Praktikum-Modul-2-Jarkom-main/franky /var/www/franky.e10.com
    cp -r Praktikum-Modul-2-Jarkom-main/super.franky /var/www/super.franky.e10.com
    cp -r Praktikum-Modul-2-Jarkom-main/general.mecha.franky /var/www/general.mecha.franky.e10.com
    ```
    
- Skypie [Pertama Kali aja]
    
    ```python
    apt-get install wget -y
    apt-get install unzip -y
    wget https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom/archive/refs/heads/main.zip
    unzip main.zip
    cd Praktikum-Modul-2-Jarkom-main/
    unzip franky.zip
    unzip general.mecha.franky.zip
    unzip super.franky.zip
    ```

## Soal 1

### Soal
EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet

### Jawaban

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled.png)

Tunjukkin Node yang udah dibuat

## Soal 2

### Soal
Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.yyy.com dengan alias www.franky.yyy.com pada folder kaizoku

### Jawaban

[ NOTE : SEMUA mkdir dan cp ADA DI script.sh ] 

EniesLobby

lakukan `nano named.conf.local` untuk mengedit

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%201.png)

`cp named.conf.local /etc/bind/named.conf.local`

disini also-notify 10.34.2.3 (water 7) dan edit /etc/bind/named.conf.local dalam water 7 sebagai slave

```python
zone "franky.e10.com" {
    type slave;
    masters { 10.34.2.2; }; // Masukan IP EniesLobby tanpa tanda petik
    file "/var/lib/bind/franky.e10.com";
};
```

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%202.png)

buka dblocal dan copy menggunakan `cp` ke root folder `franky.e10.com` edit isinya seperti berikut lalu copy ke `/etc/binc/kaizoku/franky.e10.com`

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%203.png)

lakukan `service bind9 restart` pada kedua node

buka node loguetown jangan lupa ganti nameserver pada `/etc/resolv.conf` menjadi ip enies lobby

lalu lakukan `ping [www.franky.e10.com](http://www.franky.e10.com)` pada loguetown

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%204.png)

## Soal 3

### Soal
Setelah itu buat subdomain super.franky.yyy.com dengan alias www.super.franky.yyy.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

### Jawaban

Buka lagi `/etc/bind/kaizoku/franky.e10.com` pada enieslobby dan tambahkan 2 line baru
    
![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%205.png)

Restart bind9 nya

Coba ping dari logue town domain barunya

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%206.png)

## Soal 4

### Soal
Buat juga reverse domain untuk domain utama

### Jawaban

declare di named.conf.local pada enieslobby zone baru yaitu `2.34.10.in-addr.ara` lalu copy lagi ke etc/bind/named.conf.local

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%207.png)

setelah itu buat file untuk dicopykan ke `/etc/bind/kaizoku/2.34.10.in-addr.arp` yang berisi

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%208.png)

restart bind9 service

cek di loguetown

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%209.png)

## Soal 5

### Soal
Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama

### Jawaban

Pada nomor 2 sudah kita buat dns slave untuk water7 tinggal kita test matikan enieslobby dan coba ping ke franky lagi jika tidak bisa jangan lupa tambahkan nameserver water7 pada loguetown

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20acd5184bfbff4be1a493c893912d0dd2/Untitled%2010.png)

![Untitled](Buat%20Lapres%20Shift%202%20Jarkom%20a/cd5184bfbff4be1a493c893912d0dd2/Untitled%2011.png)
