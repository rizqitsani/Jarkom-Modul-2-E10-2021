# Jarkom-Modul-2-E10-2021

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
    
    ## untuk nomor 16-17 ada tambahan command tp gak ditaro di script
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

![image](https://user-images.githubusercontent.com/77628684/139558832-786fc41c-23b4-4c9c-8565-8e17cb7a7cba.png)


Tunjukkin Node yang udah dibuat

## Soal 2

### Soal
Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.yyy.com dengan alias www.franky.yyy.com pada folder kaizoku

### Jawaban

[ NOTE : SEMUA mkdir dan cp ADA DI script.sh ] 

EniesLobby

lakukan `nano named.conf.local` untuk mengedit

![image](https://user-images.githubusercontent.com/77628684/139558837-1726fcbf-c23b-4da6-a97c-f0ac6ee20a0f.png)

`cp named.conf.local /etc/bind/named.conf.local`

disini also-notify 10.34.2.3 (water 7) dan edit /etc/bind/named.conf.local dalam water 7 sebagai slave

```python
zone "franky.e10.com" {
    type slave;
    masters { 10.34.2.2; }; // Masukan IP EniesLobby tanpa tanda petik
    file "/var/lib/bind/franky.e10.com";
};
```

![image](https://user-images.githubusercontent.com/77628684/139558846-3154f06d-1b2f-45bb-b6ab-8443e1233ef3.png)

buka dblocal dan copy menggunakan `cp` ke root folder `franky.e10.com` edit isinya seperti berikut lalu copy ke `/etc/binc/kaizoku/franky.e10.com`

![image](https://user-images.githubusercontent.com/77628684/139558852-55a1a741-14db-493e-a63d-bd509ea6a1ba.png)

lakukan `service bind9 restart` pada kedua node

buka node loguetown jangan lupa ganti nameserver pada `/etc/resolv.conf` menjadi ip enies lobby

lalu lakukan `ping [www.franky.e10.com](http://www.franky.e10.com)` pada loguetown

![image](https://user-images.githubusercontent.com/77628684/139558856-312f5a40-d95e-4541-b496-1337133efb07.png)

## Soal 3

### Soal
Setelah itu buat subdomain super.franky.yyy.com dengan alias www.super.franky.yyy.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

### Jawaban

Buka lagi `/etc/bind/kaizoku/franky.e10.com` pada enieslobby dan tambahkan 2 line baru
    
![image](https://user-images.githubusercontent.com/77628684/139558858-823965cf-0a10-4f16-8c2e-d316f14eebe8.png)

Restart bind9 nya

Coba ping dari logue town domain barunya

![image](https://user-images.githubusercontent.com/77628684/139558862-1d3226a3-9bfe-447e-842e-d42d6f0e7524.png)

## Soal 4

### Soal
Buat juga reverse domain untuk domain utama

### Jawaban

declare di named.conf.local pada enieslobby zone baru yaitu `2.34.10.in-addr.ara` lalu copy lagi ke etc/bind/named.conf.local

![image](https://user-images.githubusercontent.com/77628684/139558869-62b43c30-0e55-472a-b61b-e0e0e0ac5658.png)

setelah itu buat file untuk dicopykan ke `/etc/bind/kaizoku/2.34.10.in-addr.arp` yang berisi

![image](https://user-images.githubusercontent.com/77628684/139558873-795d1213-8b13-49d2-8852-6b190b3dbe33.png)

restart bind9 service

cek di loguetown

![image](https://user-images.githubusercontent.com/77628684/139558876-963a5ddb-3970-48c5-8bf5-18d09d162d9f.png)

## Soal 5

### Soal
Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama

### Jawaban

Pada nomor 2 sudah kita buat dns slave untuk water7 tinggal kita test matikan enieslobby dan coba ping ke franky lagi jika tidak bisa jangan lupa tambahkan nameserver water7 pada loguetown

![image](https://user-images.githubusercontent.com/77628684/139558882-76a00d1b-dc20-4573-9f2d-dcdf8b2dfbef.png)


## Soal 6

### Soal

Setelah itu terdapat subdomain mecha.franky.yyy.com dengan alias www.mecha.franky.yyy.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo

### Jawaban

Pada enies lobby tambahkan line baru pada file franky.e10.com

![image](https://user-images.githubusercontent.com/65166398/139536758-fc0fcd61-a1d8-4665-882d-39bf35436f26.png)


Lalu tambahkan pada water7 named local conf zone delegasi seperti dibawah

![image](https://user-images.githubusercontent.com/65166398/139536818-14139b57-fa2f-4ef9-9a5a-7686fc58e488.png)

Buka loguetown dan jalankan ping **www.mecha.franky.yyy.com**

![image](https://user-images.githubusercontent.com/65166398/139536799-17fdc286-def5-4df4-be30-7cf4dc2565e6.png)


## Soal 7

### Soal

Untuk memperlancar komunikasi Luffy dan rekannya, dibuatkan subdomain melalui Water7 dengan nama general.mecha.franky.yyy.com dengan alias www.general.mecha.franky.yyy.com yang mengarah ke Skypie

### Jawaban

Pada water7 [mecha.franky.e10.com](http://mecha.franky.e10.com) tambahkan 2 line baru

![image](https://user-images.githubusercontent.com/65166398/139536876-71ab1bf7-3422-4836-8135-49ed3cad9008.png)


Ping dari logue town

![image](https://user-images.githubusercontent.com/65166398/139537021-6d015d63-8e38-4902-a86c-a64e9462dd73.png)


## Soal 8

### Soal

Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com

### Jawaban

Taruh file yang dibutuhkan dalam skypie

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

Konfigurasikan [franky.e10.com](http://franky.e10.com) pada enies lobby seperti  berikut

![image](https://user-images.githubusercontent.com/65166398/139537044-37d571da-b05c-4700-b8ac-2f1c5f617021.png)

Install apache2 dan php di water7

Buka node skypie

Copy `/etc/apache2/sites-available/000-default.conf` ke folder webserver dengan nama file `franky.e10.com.conf` nano dan edit isinya sesuai permintaan

![image](https://user-images.githubusercontent.com/65166398/139537078-b66b8a8f-e6a4-4dce-af8b-9e3a4e540ee1.png)


Setelah itu copykan file itu lagi ke direktori `cp webserver/franky.e10.com.conf /etc/apache2/sites-available/franky.e10.com.conf`
jangan lupa untuk aktifkan konfigurasi

`a2ensite [franky.e10.com](http://franky.e10.com/)`

Lalu restart apachenya

`service apache2 restart`

Coba dari logue town

`lynx www.franky.e10.com`

![image](https://user-images.githubusercontent.com/65166398/139537096-f8556d5f-a512-430b-9f1a-1e8f59ccd81a.png)


Loguetown sudah berhasil masuk tetapi belum ada file apa-apa copy file franky yang sudah didownload kedalam folder `/var/www/franky.e10.com`

Coba lynx lagi ke franky.e10.com

![image](https://user-images.githubusercontent.com/65166398/139537107-7ec44619-b26c-41a8-9dbd-d2e22f171e18.png)


## Soal 9

### Soal

Setelah itu, Luffy juga membutuhkan agar url www.franky.yyy.com/index.php/home dapat menjadi menjadi www.franky.yyy.com/home

### Jawaban

Buka folder webserver di skypie dan tambahkan alias pada conf

![image](https://user-images.githubusercontent.com/65166398/139537158-aaf54b59-8185-4176-a8a0-c96f690b05b8.png)


Jangan lupa copy kan lagi ke

`cp webserver/franky.e10.com.conf /etc/apache2/sites-available/franky.e10.com.conf`

Jangan lupa untuk restart server apache

Sekarang buka loguetown dan lakukan lynx ke yang diminta

![image](https://user-images.githubusercontent.com/65166398/139537218-269484a6-1b66-4d15-897f-2db9916df559.png)


![image](https://user-images.githubusercontent.com/65166398/139537230-85dc5c79-a221-4dc7-8c90-b0a44cbefe16.png)


## Soal 10

### Soal

Setelah itu, pada subdomain www.super.franky.yyy.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.yyy.com

### Jawaban

Masuk folder webserver pada skypie lagi dan copy file franky.e10.com.conf menjadi `[super.franky.e10.com](http://super.franky.e10.com)` isi seperti berikut

![image](https://user-images.githubusercontent.com/65166398/139537252-19681e25-4efb-4dba-86a8-f8420699adfa.png)


Lakukan cp [super.franky.e10.com](http://super.franky.e10.com) ke `/etc/apache2/sites-available/super.franky.e10.com.conf` jangan lupa mkdir folder tersebut sebelumnya

cp webserver/super.franky.e10.com.conf `/etc/apache2/sites-available/`

Lalu `a2ensite .super.franky.e10.com.conf` dan restart server apachenya

![image](https://user-images.githubusercontent.com/65166398/139537268-f4a471a4-436d-4b50-8530-2c2a5478ec03.png)


![image](https://user-images.githubusercontent.com/65166398/139537278-5ce53ffb-5211-4095-8546-5e6061f5dd79.png)


Jangan lupa untuk copy file yang diminta ke var/www/super.franky.e10.com

Lynx lagi dari loguetown

![image](https://user-images.githubusercontent.com/65166398/139537292-b4af8b1b-ac22-4eac-b99f-a5ebe5fd92b6.png)


## Soal 11

### Soal
Akan tetapi, pada folder /public, Luffy ingin hanya dapat melakukan directory listing saja

### Jawaban

Buka lagi folder webserver pada skypie edit dan lalu nanti copy seperti sebelum-sebelumnya

`super.franky.e10.com.conf`

![image](https://user-images.githubusercontent.com/65166398/139537308-14f22bb8-498c-465e-b88d-2ede34c5bde7.png)


Save, copy, restart apache

![image](https://user-images.githubusercontent.com/65166398/139537320-07ba712c-59b4-47b8-a1a3-5b0af76d5066.png)

## Soal 12

### Soal
Tidak hanya itu, Luffy juga menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache

### Jawaban

di node skypie edit super.franky.e10.com.conf dan tambahkan line berikut
![image](https://user-images.githubusercontent.com/77628684/139558958-6a679daa-e326-4aa9-9cbe-8743ee891c22.png)
setelah itu coba lynx dari loguetown dengan akhiran asal
![image](https://user-images.githubusercontent.com/77628684/139558971-428bc73c-db45-4814-9ca9-a93b3e3911bf.png)


## Soal 13

### Soal
Luffy juga meminta Nami untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset www.super.franky.yyy.com/public/js menjadi www.super.franky.yyy.com/js

### Jawaban

di node skypie edit super.franky.e10.com.conf dan tambahkan line berikut 

![image](https://user-images.githubusercontent.com/77628684/139558982-3862716f-8acf-41f7-8f6e-0934d4fecb16.png)

restart dan lalu coba dari loguetown

![image](https://user-images.githubusercontent.com/77628684/139558990-62b9b31f-a093-4d6a-95ef-7629ca3eca7c.png)


## Soal 14

### Soal
Dan Luffy meminta untuk web www.general.mecha.franky.yyy.com hanya bisa diakses dengan port 15000 dan port 15500

### Jawaban

di skypie buat config baru general.mecha.e10.com-15000.conf

![image](https://user-images.githubusercontent.com/77628684/139558996-ddd8d362-1b3f-4dc2-adea-bc05cb0facd4.png)

buat juga copyan ini untuk 15500 config. (2 2 nya config masukin ke sites-available kalo udah)
tambah listen port pada `/etc/apache2/ports.conf`

![image](https://user-images.githubusercontent.com/77628684/139559005-eec71b00-049c-4d94-b291-2bb7c71bad63.png)

a2ensite kedua config baru tersebut lalu restart ApAcHeNyA.
jgn lupa copy file mecha yang didownload kedalam var/www
`lynx [http://www.general.mecha.franky.e10.com:15000/](http://www.general.mecha.franky.e10.com:15000/)`
`lynx [http://www.general.mecha.franky.e10.com:15500/](http://www.general.mecha.franky.e10.com:15000/)`

![image](https://user-images.githubusercontent.com/77628684/139559011-caf12831-828a-4573-9035-0853ad836873.png)


## Soal 15

### Soal
dengan autentikasi username luffy dan password onepiece dan file di /var/www/general.mecha.franky.yyy

### Jawaban

bikin password di skypie buat apache2
REFERENSI : [https://httpd.apache.org/docs/2.4/programs/htpasswd.html](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)
`htpasswd -b -c /etc/apache2/.htpasswd luffy onepiece`
lalu edit config general mecha 15000 dan 15500

![image](https://user-images.githubusercontent.com/77628684/139559022-56b748b5-2c78-442b-8631-4440687eb77e.png)

restart apache dan coba dari loguetown
akan keluar permintaan inputan sbb

![image](https://user-images.githubusercontent.com/77628684/139559025-113b2386-8d90-4a2c-829c-b790da6ec1ba.png)

masukkan username luffy enter lalu masukan password onepice bam!
kebuka deh

![image](https://user-images.githubusercontent.com/77628684/139559034-5a0bd8ef-cbbc-48c5-9a1f-608be313f78a.png)


## Soal 16

### Soal
 Dan setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.yyy.com

### Jawaban

buka node Skypie
kita akan menggunakan rewrite pada apache
`a2enmod rewrite`
nano /var/www/franky.e10.com/.htaccess [ini gaada discript] isi seperti berikut

![image](https://user-images.githubusercontent.com/77628684/139559045-9e61a05a-fcd7-45c7-af24-e54240242d82.png)

```
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.34\.2\.4$
RewriteRule ^(.*)$ http://www.franky.e10.com/$1 [L,R=301]
```
lalu rubah isi default /etc/apache2/sites-available/000-default.conf menjadi
![image](https://user-images.githubusercontent.com/77628684/139559052-41fcae70-ee10-46ea-9f13-b556ff6cd256.png)

save, restart test dari loguetown

![image](https://user-images.githubusercontent.com/77628684/139559064-33b5e82a-7cac-47f8-9a9c-926a019e9e86.png)

## Soal 17

### Soal
Dikarenakan Franky juga ingin mengajak temannya untuk dapat menghubunginya melalui website www.super.franky.yyy.com, dan dikarenakan pengunjung web server pasti akan bingung dengan randomnya images yang ada, maka Franky juga meminta untuk mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png. Maka bantulah Luffy untuk membuat konfigurasi dns dan web server ini!

### Jawaban

pada skypie
`nano /var/www/super.franky.e01.com/.htaccess`

```
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_URI} !\bfranky.png\b
RewriteRule franky http://super.franky.e10.com/public/images/franky.png$1 [L,R=301]
```
lalu ganti config pada sites-available/super.franky dengan menambah AllowOverride All
![image](https://user-images.githubusercontent.com/77628684/139559078-2737d320-edaf-4bfb-ab7c-cd0315307308.png)

kalo sudah save lalu jangan lupa
`a2enmod rewrite`
dan juga jangan lupa restart apache
lalu coba di loguetown lynx superfranky dengan belakangan tulisan asal yang memiliki substring "franky" didalamnya

![image](https://user-images.githubusercontent.com/77628684/139559081-df08e0e1-9ea1-4cff-9e0c-0ad7b7f63070.png)




# Kendala 
1. Jenis soal membuat pembagian kerja agak sulit
2. Waktu praktikum agak kurang dibanding panjang soal
