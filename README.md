# Jarkom_Modul3_Lapres_C03

- Brananda Denta WP - 05111840000143
- R. Dafa Berlian Denmar - 05111840000149

## Outline

+ [Soal 1](#soal-1)
+ [Soal 2](#soal-2)
+ [Soal 3](#soal-3)
+ [Soal 4](#soal-4)
+ [Soal 5](#soal-5)
+ [Soal 6](#soal-6)
+ [Soal 7](#soal-7)
+ [Soal 8](#soal-8)
+ [Soal 9](#soal-9)
+ [Soal 10](#soal-10)
+ [Soal 11](#soal-11)
+ [Soal 12](#soal-12)

## Soal 1

### Langkah Pengerjaan
- Membuat file `topologi.sh` yang berisi topologi jaringan sesuai permintaan soal, dimana terdapat 1 router (SURABAYA), 3 switch (switch1, switch2, switch3), 4 client (SIDOARJO, GRESIK, BANYUWANGI, MADIUN), dan 3 server (MALANG, MOJOKERTO, TUBAN).

![no 1](/img/putty.jpg)

- Jalankan `bash topologi.sh` untuk membuat uml sesuai dengan topologi yang diatur pada `topologi.sh`
- Ubah isi dari isi dari file `/etc/network/interfaces` pada setiap uml sesuai dengan gambar dibawah ini.

- SURABAYA

![no 1](/img/surabayainterface.jpg)

- MALANG

![no 1](/img/malanginterface.jpg)

- MOJOKERTO

![no 1](/img/mojointerface.jpg)

- TUBAN

![no 1](/img/tubaninteface.jpg)

- GRESIK

![no 1](/img/gresikinterface.jpg)

- SIDOARJO

![no 1](/img/sidoarjointerface.jpg)

- BANYUWANGI

![no 1](/img/banyuwangiinterface.jpg)

- MADIUN

![no 1](/img/madiuninterface.jpg)

- Jalankan `service networking restart` pada setiap client agar bisa mendapatkan IP
- Jalankan `ifconfig` untuk memeriksa IP yang didapatkan setiap client

![no 1](/img/ifconfig.jpg)

## Soal 2
### Langkah Pengerjaan

- Install `isc-dhcp-relay` pada uml SURABAYA (**DHCP Relay**)
- Ubah konfigurasi yang ada pada file `/etc/default/isc-dhcp-relay` menjadi seperti gambar dibawah ini

![no 2](/img/semeruc03.pw.jpg)

- Jalankan `service isc-dhcp-relay restart`

## Soal 3

### Langkah Pengerjaan

- Jalankan perintah `nano /etc/bind/semeru/semeruc03.pw` dan setting seperti dibawah

### Screenshot
![no 3](/img/semeruc03.pw.jpg)

- Jalankan perintah `service bind9 restart` pada UML Malang
- tes ping penanjakan.semeruc03.pw pada UML client

### Screenshot
![no 3](/img/pingpenanjakan.jpg)

## Soal 4

### Langkah Pengerjaan

- Edit file **/etc/bind/named.conf.local** pada *MALANG* dan tambahkan konfigurasi untuk zone 77.151.10.in-addr.arpa.

### Screenshot
![no 4](/img/namedConfLocalMalang.jpg)

- lalu copy file db.local dengan perintah `cp /etc/bind/db.local /etc/bind/semeru/77.151.10.in-addr.arpa` lalu kita edit seperti dibawah

### Screenshot
![no 4](/img/77.jpg)

- restart bind9 pada *MALANG*

```sh
service bind9 restart
```

- tes pada UML client host -t PTR 10.151.77.34

### Screenshot
![no 4](/img/host-TGresik.jpg)

## Soal 5
### Langkah Pengerjaan

- Setting pada UML MALANG, Edit file `/etc/bind/named.conf.local` dan tambahkan type, notify, dan also-notify seperti gambar berikut

### Screenshot

![no 5](/img/namedConfLocalMalang.jpg)

- Lakukan restart bind9

```sh
service bind9 restart
```

- Pada UML MOJOKERTO, lakukan update dan install bind9

```sh
apt-get update
apt-get install bind9 -y
```

- lalu ubah file **/etc/bind/named.conf.local** seperti dibawah

### Screenshot

![no 5.1](/img/namedConfLocalMojo.jpg)

- Lakukan restart bind9

```sh
service bind9 restart
```

- Untuk testing, Pada server MALANG silahkan matikan service bind9

```sh
service bind9 stop
```

- Pada client GRESIK pastikan pengaturan nameserver mengarah ke IP MALANG dan IP MOJOKERTO

### Screenshot

![no 5](/img/resolvGresik.jpg)

- tes ping pada UML Client (GRESIK)
### Screenshot

![no 5](/img/pingSemeru.jpg)

## Soal 6

### Langkah Pengerjaan

- Setting pada UML Malang pada file /etc/bind/semeru/semeruc03.pw, tambahkan subdomain gunung

### Screenshot
![no 6](/img/semeruc03.pw.jpg)

- Kemudian edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah:

### Screenshot

![no 6.1](/img/namedConfLocalMalang.jpg)

- Restart service bind

```sh
service bind9 restart
```

- Setting pada UML Mojokerto pada file /etc/bind/named.conf.local

### Screenshot
![no 6](/img/namedConfLocalMojo.jpg)

- Kemudian buat direktori dengan nama delegasi

- Copy db.local ke direktori pucang dan edit namanya menjadi gunung.semeruc03.pw, lalu ubah menjadi seperti berikut.

### Screenshot
![no 6](/img/gunungSemeru.jpg)

- Restart service bind

```sh
service bind9 restart
```

- Untuk testing, ping gunung.semeruc03.pw pada UML client

### Screenshot
![no 6](/img/pingGunung.jpg)

## Soal 7
### Langkah Pengerjaan

- Buat subdomain naik.gunung.semeruc03.pw dengan mengatur file /etc/bind/delegasi/gunung.semeruc03.pw pada UML Mojokerto

### Screenshot
![no 7](/img/gunungSemeru.jpg)

- Restart service bind

```sh
service bind9 restart
```

- Cek ping naik.gunung.semeruc03.pw pada UML client

### Screenshot
![no 7.1](/img/pingNaik.jpg)

## Soal 8

### Langkah Pengerjaan

- Install php dan apache2
- copy file default menjadi semeruc03.pw.conf pada directory /etc/apache2/sites-available
- Tambahkan ServerAlias dan ServerName, serta atur DocumentRoot

### Screenshot
![no 8](/img/semeruConf.jpg)

- wget 10.151.36.202/semeru.pw.zip pada directory /var/www/ lalu di unzip dan rename menjadi semeruc03.pw
- a2ensite semeruc03.pw untuk enable site dan service apache2 restart
- akses website semeruc03.pw pada browser
### Screenshot
![no 8](/img/webUtama.jpg)

## Soal 9
### Langkah Pengerjaan

- Pindah ke directory /var/www/semeruc03.pw dan buat file .htaccess dengan isi file
### Screenshot

![no 9](/img/homehtaccess.jpg)

- Menjalankan perintah a2enmod rewrite untuk mengaktifkan module rewrite.

- Pindah ke directory /etc/apache2/sites-available kemudian buka file semeruc03.pw.conf dan tambahkan
```
<Directory /var/www/semeruc03.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```

### Screenshot

![no 9](/img/semeruConf.jpg)

- Restart apache dengan perintah " service apache2 restart "

### Screenshot

![no 9](/img/indexHome.jpg)
![no 9](/img/homeShow.jpg)


## Soal 10
### Langkah Pengerjaan
- Buat directory website dengan perintah " mkdir /var/www/penanjakan.semeruc03.pw "
- Pindah ke direktori /etc/apache2/sites-available dan copy file default ke file penanjakan.semeruc03.pw.conf
- Edit file penanjakan.semeruc03.pw.conf

### Screenshot

![no 10](/img/penanjakanAtas.jpg)

- Aktifkan konfigurasi dengan perintah " a2ensite penanjakan.semeruc03.pw "
- Download file pendukung dengan wget 10.151.36.202/penanjakan.semeruc03.pw.zip lalu unzip ke directory /var/www/penanjakan.semeruc03.pw

### Screenshot

![no 10](/img/lsPenanjakan.jpg)

## Soal 11
### Langkah Pengerjaan

- tambahkan konfigurasi pada file /etc/apache2/sites-available/penanjakan.semeruc03.pw.conf sesuai dengan gambar :

### Screenshot

![no 11](/img/penanjakanAllAtas.jpg)

- Sehingga menjadi seperti ini pada tampilan website:

### Screenshot

![no 11](/img/penanjakanShowAll.jpg)

![no 11](/img/penanjakanShowError.jpg)

![no 11](/img/penanjakanShowPub.jpg)

![no 11](/img/cssforb.jpg)

![no 11](/img/imagesforb.jpg)

![no 11](/img/jsforb.jpg)

## Soal 12
### Langkah Pengerjaan

- Tambahkan ErrorDocument dan pemeriksaan redirect status pada file /etc/apache2/sites-enabled/penanjakan.semeruc03.pw.conf

### Screenshot

![no 12](/img/404conf.jpg)

Hasil:

![no 12](/img/404page.jpg)
