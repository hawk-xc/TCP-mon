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

dan masuk lagi ke konfigurasi pada file

```bash
nano /etc/apache2/sites-available/000-default.conf
```

lalu ubah konfigurasi pada `<Virtualhost *:80>` menjadi `<Virtualhost *:8888>`

```                                                            
<VirtualHost *:8888>
```

start dan restart konfigurasi pada web server dengan perintah

```bash
systemctl start apache2
systemctl restart apache2
```

### jalankan tcp-mon

sebelumnya silakan check ip address OS linux teman-teman, dengan perintah

```bash
ifconfig
```
```
enp2s0f1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.15  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::f276:1cff:fec2:542c  prefixlen 64  scopeid 0x20<link>
        ether f0:76:1c:c2:54:2c  txqueuelen 1000  (Ethernet)
        RX packets 1245105  bytes 328954839 (328.9 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 559003  bytes 2553832235 (2.5 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 43  base 0x5000  
```

jalankan tools tcp-mon dengan perintah

```bash
./build/tcpmon.sh
```

![Screenshot from 2022-02-16 23-05-21](https://user-images.githubusercontent.com/92193431/154382560-6180ca43-9957-438e-ac2c-01f0afec2500.png)

pada jendela workspace, silakan teman-teman masuk navbar admin, disini isikan port listen, hostname dan target port. disini saya menggunakan listen port `8080`, target hostname `192.168.2.15` dan target port `8888`.


![Screenshot from 2022-02-17 07-57-05](https://user-images.githubusercontent.com/92193431/154383565-a6454239-8511-47a3-8de6-ec12dc3ae238.png)

dan sekarang silakan teman-teman coba akses web server menggunakan  port 8080 pada sisi client


![Screenshot from 2022-02-17 07-54-56](https://user-images.githubusercontent.com/92193431/154383383-23b2c62d-f7c8-4c3e-9b89-a03bde8157f2.png)


