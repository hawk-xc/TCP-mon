# TCP-mon
terkadang untuk keperluan analisis sebuah data pada jaringan komputer, kita memerlukan tools untuk membaca atau menganalisis sebuah data menggunakan tools salah satunya ialah TCP-Mon, tools ini memanfaatkan protokol TCP header untuk membaca atau menganalisis sebuah data yang lalu lalang pada jaringan komputer.

Protokol TCP merupakan sebuah protokol pada jaringan komputer yang bersifat connection-oriented atau menjamin data terkirim sepenuhnya, lengkap, berurutan, dan terjamin. TCP memiliki sebuah header yang berisikan tentang tipe data, jenis, koneksi yang menjalin, port dan lain sebagainya, disini kita bisa membaca header TCP tersebut salah satunya menggunakan tools TCP-mon. tools ini cukup simple untuk digunakan.

pada modul kali ini saya akan mempraktikan cara menginstall dan cara mengimplementasikan tools yang satu ini.

### installasi

Sebelumnya saya menggunakan distro linux Ubuntu 20.04 LTS (focal fossa) GUI, teman-teman juga bisa menggunakan distro linux yang lainnya. silakan login menggunakan super user account

```bash
sudo su
```

lakukan update repository

```bash
apt-get update
```

baiklah disini silakan teman-teman melakukan installasi terhadap web server, disini saya menggunakan web server `Apache2`.

```bash
apt-get install apache2
```

jika sudah silakan install package berikut

```bash
apt-get install wget openjdk-8-jre
```

unduh tcp-mon pada website resminya dan ekstrak dengan perintah

```bash
wget http://archive.apache.org/dist/ws/tcpmon/1.0/tcpmon-1.0-bin.zip
unzip tcpmon-1.0-bin.zip
```

konfigurasi port listen pada web server pada file konfigurasi, edit dengan nano text editor.

```bash
nano /etc/apache2/ports.conf
```

lalu ubah port `listen 80` menjadi `listen 8888`

```
Listen 8888

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
```



