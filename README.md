# Jarkom_Modul3_Lapres_C03

- Brananda Denta WP - 05111840000143
- R. Dafa Berlian Denmar - 05111840000149

## Outline

+ [Soal 1](#soal-1)
+ [Soal 2](#soal-2)
+ [Soal 3](#soal-3---6)
+ [Soal 4](#soal-3---6)
+ [Soal 5](#soal-3---6)
+ [Soal 6](#soal-3---6)
+ [Soal 7](#soal-7)
+ [Soal 8](#soal-8---9)
+ [Soal 9](#soal-8---9)
+ [Soal 10](#soal-10)
+ [Soal 11](#soal-11)
+ [Soal 12](#soal-12)

## Soal 1

### Langkah Pengerjaan
- Membuat file `topologi.sh` yang berisi topologi jaringan sesuai permintaan soal, dimana terdapat 1 router (SURABAYA), 3 switch (switch1, switch2, switch3), 4 client (SIDOARJO, GRESIK, BANYUWANGI, MADIUN), dan 3 server (MALANG, MOJOKERTO, TUBAN).

![no 1](/img/putty.jpg)

- Jalankan `bash topologi.sh` untuk membuat UML sesuai dengan topologi yang diatur pada `topologi.sh`
- Ubah isi dari isi dari file `/etc/network/interfaces` pada setiap UML sesuai dengan gambar dibawah ini.

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

- Jalankan `service networking restart` pada setiap UML

## Soal 2
### Langkah Pengerjaan

- Install `isc-dhcp-server` pada UML TUBAN (**DHCP Server**) dan `isc-dhcp-relay` pada UML SURABAYA (**DHCP Relay**)
- Pada UML **SURABAYA**, ubah konfigurasi yang ada pada file `/etc/default/isc-dhcp-relay` menjadi seperti gambar dibawah ini

![no 2](/img/surabayaispdhcp1.png)

- Jalankan `service isc-dhcp-relay restart`

- Pada UML **TUBAN**, ubah konfigurasi yang ada pada file `/etc/default/isc-dhcp-server` menjadi seperti gambar dibawah ini

![no 2](/img/tubaniscdhcp.jpg)

- jalankan `service isc-dhcp-server restart`

## Soal 3 - 6

### Langkah Pengerjaan

- Pada UML TUBAN (**DHCP Server**), jalankan perintah `nano /etc/dhcp/dhcpd.conf` dan setting seperti dibawah

![no 3](/img/tubandhcpd.jpg)

- Jalankan perintah `service isc-dhcp-server restart`
- Jalankan `service networking restart` pada setiap client agar bisa mendapatkan IP
- Jalankan `ifconfig` untuk memeriksa IP yang didapatkan setiap client

![no 3](/img/ifconfig.jpg)

## Soal 7
### Langkah Pengerjaan
- Install `squid` pada UML MOJOKERTO dengan menjalankan 

```sh
apt-get install squid
```

- Periksa status squid dengan menjalankan

```sh
service squid status
```

![no 7](/img/mojosquidstatus.jpg)

- Backup terlebih dahulu file konfigurasi default yang disediakan Squid.

```sh
mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
```

- Buat konfigurasi baru dengan mengetikkan

```sh
nano /etc/squid/squid.conf
```

- Kemudian, pada file config yang baru, ketikkan script seperti gambar berikut

![no 7](/img/mojosquidconf.jpg)

- Restart squid dengan cara mengetikkan perintah:

```sh
service squid restart
```

- Ubah pengaturan proxy browser. Gunakan **IP MOJOKERTO** sebagai host dan isikan port 8080

![no 7](/img/proxyport.jpg)

- Install `apache2-utils` pada UML MOJOKERTO dengan menjalankan 

```sh
apt-get install apache2-utils
```

- Buat user `userta_c03` dengan password `inipassw0rdta_c03` dengan menjalankan perintah berikut 

```sh
htpasswd -c /etc/squid/passwd userta_c03
```

- Tambahkan konfigurasi untuk user login dengan meminta autentikasi serta menolak semua akses yang bukan berasal dari user seperti dibawah ini 

![no 7](/img/mojosquidconf.jpg)

- Restart squid
- Mencoba mengakses website apapun dan akan muncul pop up permintaan login seperti gambar dibawah ini

![no 7](/img/login.jpg)

## Soal 8 - 9

### Langkah Pengerjaan

- Buat file baru bernama acl.conf di folder squid

```sh
nano /etc/squid/acl.conf
```

- Isikan file seperti gambar dibawah ini

![no 8](/img/mojotimeacl.jpg)

- Tambahkan konfigurasi untuk file acl pada file konfigurasi squid dengan menambahkan include acl serta hanya memperbolehkan akses pada jadwal yang diatur pada alias `TA`, `BIM`, `BING` pada file acl

```sh
nano /etc/squid/squid.conf
```

![no 8](/img/mojosquidconf.jpg)


- Simpan file tersebut. Kemudian restart squid.
- Coba mengakses website apapun pada jadwal yang tidak diperbolehkan

![no 8](/img/forbidden.jpg)

## Soal 10
### Langkah Pengerjaan
- Tambahkan acl `gaboleh` yang merupakan `dstdomain` yang menuju ke www.google.com pada `squid.conf`
- tolak semua akses ke `gaboleh` dan arahkan ke http://monta.if.its.ac.id 

```sh
nano /etc/squid/squid.conf
```
![no 10](/img/mojosquidconf.jpg)

- Simpan file tersebut. Kemudian restart squid.
- Coba mengakses google.com

![no 10](/img/login.jpg)

- setelah login, kita akan diarahkan ke http://monta.if.its.ac.id

![no 10](/img/redirectmonta.jpg)

## Soal 11
### Langkah Pengerjaan

- Masuk ke folder `/usr/share/squid/errors/en` dan download error page dengan menjalankan `wget 10.151.36.202/ERR_ACCESS_DENIED`

![no 11](/img/nomer11.jpg)

- Rename file `ERR_ACCESSS_DENIED` dan rename file yang baru saja didownload yaitu `ERR_ACCESSS_DENIED.1` menjadi `ERR_ACCESSS_DENIED`

- Untuk mencoba, ubah file konfigurasi squid menjadi seperti gambar dibawah ini

![no 11](/img/mojosquidconfdenyallfinal.jpg)

- Simpan file tersebut. Kemudian restart squid.
- Coba akses website apapun, dan akan diarahkan ke halaman forbidden

![no 11](/img/forbidden2.jpg)

- Kembalikan konfigurasi squid seperti sebelumnya setelah mencoba
- Restart squid

## Soal 12
### Langkah Pengerjaan

- Install bind9 pada UML MALANG

```sh
apt-get install bind9 -y
```

- Buat domain janganlupa-ta.c03.pw

```sh
nano /etc/bind/named.conf.local
```

![no 12](/img/malangnamedconflocal.jpg)

- Buat folder jarkom di dalam /etc/bind

```sh
mkdir /etc/bind/jarkom
```

- Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi janganlupa-ta.c03.pw

```sh
cp /etc/bind/db.local /etc/bind/jarkom/janganlupa-ta.c03.pw
```

- Kemudian buka file janganlupa-ta.c03.pw dan edit seperti gambar berikut

![no 12](/img/malangjanganlupata.jpg)

- Restart bind9 dengan perintah `service bind9 restart`

- Coba ping `janganlupa-ta.c03.pw` dari client

![no 12](/img/gresikpingjanganlupata.jpg)

- Ubah pengaturan proxy browser. Gunakan `janganlupa-ta.c03.pw` sebagai host dan isikan port 8080

![no 12](/img/proxyjanganlupata.jpg)

- Uji coba beberapa hal yang telah bisa dilakukan sebelumnya, seperti mengakses google.com yang akan diarahkan ke http://monta.if.its.ac.id

![no 12](/img/login.jpg)

![no 12](/img/redirectmonta.jpg)
