# Laporan_Praktikum_Modul_5_A13

Setelah kalian mempelajari semua modul yang telah diberikan, Bibah ingin meminta bantuan <br/>
untuk terakhir kalinya kepada kalian.Dan kalian dengan senang hati mau membantu Bibah. <br/>
## (A) Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan <br/>
Bibah seperti dibawah ini : <br/>

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/1.png)

Keterangan : SURABAYA diberikan IP TUNTAP <br/>

MALANG merupakan DNS Server diberikan IP DMZ <br/>
MOJOKERTO merupakan DHCP Server diberikan IP DMZ <br/>
MADIUN dan PROBOLINGGO merupakan WEB Server <br/>
Setiap Server diberikan memory sebesar 128M <br/>
Client dan Router diberikan memori sebesar 96M <br/>
Jumlah host pada subnet SIDOARJO 200 Host <br/>
Jumlah host pada subnet GRESIK 210 Host <br/>

### Penyelesaian :

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/2.png)

## (B) karena kalian telah mempelajari Subnetting dan Routing, Bibah meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM. Setelah melakukan subnetting,  <br/>

## (C) kalian juga diharuskan melakukan routing agar setiap perangkat pada jaringan tersebut dapat terhubung. <br/>

### Penyelesaian <br/>

**Menggunakan Teknik CIDR** <br/>

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/3.png)

**Tree**

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/4.png)

**Subneting**  <br/>
Masukan perintah  nano /etc/network/interfaces pada setiap UML dan masukan IP sesuai yang telah dibuat
- SURABAYA

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/5.png)

- BATU

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/6.png)

- GRESIK

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/7.png)

- PROBOLINGGO

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/8.png)

- MALANG

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/9.png)

- SIDOARJO

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/10.png)

- MADIUN

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/11.png)

- KEDIRI

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/12.png)

- MOJOKERTO

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/13.png)

**Kemudian lakukan konfigurasi sebagai  berikut** <br/>
- MOJOKERTO <br/>
*Install DHCP SERVER dengan mengetikkan apt-get install isc-dhcp-server* <br/>

- MALANG <br/>
a. Buat domain di malang dengan Langkah sebagai  berikut <br/>

b. Buka MALANG dan update package lists dengan menjalankan command:   <br/>
*apt-get update* <br/>

c. Setalah melakukan update silahkan install aplikasi bind9 pada MALANG dengan perintah: <br/>
*apt-get install bind9* <br/>

d. Lakukan perintah pada MALANG. Isikan seperti berikut (Konfigurasi berikut untuk nomor 6): <br/>
 *nano /etc/bind/named.conf.local* <br/>

e. Isikan configurasi domain  sesuai dengan syntax berikut: <br/>
*zone "jarkom2020.com" { <br/>
	type master; <br/>
	file "/etc/bind/jarkom/jarkom2020.com"; <br/>
};* <br/>

f. Buat folder jarkom di dalam /etc/bind <br/>
*mkdir /etc/bind/jarkom* <br/>

g. Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi domainmu.com <br/>
*cp /etc/bind/db.local /etc/bind/jarkom/jarkom2020.com* <br/>

h. Kemudian buka file domainmu.com dan edit IP MALANG menjadi 192.168.6.1 (IP TEMP) <br/>
*nano /etc/bind/jarkom/jarkom2020.com* <br/>

i. Restart bind9 dengan perintah <br/>
*service bind9 restart* <br/>

- BATU dan KEDIRI <br/>
Install dahulu DHCP Relay dengan mengikuti perintah berikut <br/>
*apt-get install isc-dhcp-relay* <br/>
kemudian masukan IP MOJOKERTO (10.151.73.115) <br/>

- PROBOLINGGO DAN MADIUN <br/>
Untuk web server masukan perintah berikut <br/>
*apt-get install apache2*  <br/>
*apt-get install php5* <br/>
 
- SURABAYA

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/14.png)

## (D) Tugas berikutnya adalah memberikan ip pada subnet SIDOARJO dan GRESIK secara dinamis <br/>
menggunakan bantuan DHCP SERVER (Selain subnet tersebut menggunakan ip static). Kemudian <br/>
kalian mengingat bahwa kalian harus setting DHCP RELAY pada router yang menghubungkannya, <br/>
seperti yang kalian telah pelajari di masa lalu. <br/>
Untuk pengaturan DHCP Sebagai berikut <br/>

![Gambar](https://github.com/riskiferdian/Laporan_Praktikum_Modul_5_A13/blob/main/images/15.png)

## (1) Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi SURABAYA menggunakan iptables, namun Bibah tidak ingin kalian menggunakan MASQUERADE.  <br/>

### Penyelesaian : <br/>
Pada SURABAYA masukkan perintah berikut <br/>
iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.72.58 <br/>

## (2) Kalian diminta untuk mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan.  <br/>

### Penyelesaian : <br/>
Untuk no 2 nantinya akan di override no 7 <br/>
Pada SURABAYA masukan perintah berikut <br/>
iptables -A FORWARD -p tcp --dport 22 -d 10.151.73.112/29 -i eth0 -j DROP <br/>

## (3) Karena tim kalian maksimal terdiri dari 3 orang, Bibah meminta kalian untuk membatasi DHCP <br/>
dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana 
saja menggunakan iptables pada masing masing server, selebihnya akan di DROP. <br/>
kemudian kalian diminta untuk membatasi akses ke MALANG yang berasal dari SUBNET <br/>
SIDOARJO dan SUBNET GRESIK dengan peraturan sebagai berikut: <br/>

### Penyelesaian : <br/>
Pada nomor 3 nantinya akan di override no 7 <br/> <br/>
Pada MALANG dan MOJOKERTO masukan perintah berikut <br/>
iptables -A FORWARD -p tcp --dport 22 -d 10.151.73.112/29 -i eth0 -j DROP <br/>

## (4) Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.

### Penyelesaian : <br/>
Pada MALANG masukan perintah berikut <br/>
iptables -A INPUT -s 192.168.4.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT <br/>
iptables -A INPUT -s 192.168.4.0/24 -j REJECT <br/>

## (5) Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya.
Selain itu paket akan di REJECT. <br/>
Karena kita memiliki 2 buah WEB Server,  <br/>

### Penyelesaian : <br/>
Pada MALANG masukan perintah berikut <br/>
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 17:00 --timestop 00:00 -j ACCEPT <br/>
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 00:00 --timestop 07:00 -j ACCEPT <br/>
iptables -A INPUT -s 192.168.0.0/24 -j REJECT <br/>

## (6) Bibah ingin SURABAYA disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.

### Penyelesaian : <br/>
Pada SURABAYA masukan perintah berikut <br/>
iptables -A PREROUTING -t nat -p tcp -d 192.168.6.1 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.1.2 <br/>
iptables -A PREROUTING -t nat -p tcp -d 192.168.6.1 --dport 80 -j DNAT --to-destination 192.168.1.3 <br/>
iptables -t nat -A POSTROUTING -p tcp -d 192.168.1.2 --dport 80 -j SNAT --to-source 192.168.6.1 <br/>
iptables -t nat -A POSTROUTING -p tcp -d 192.168.1.3 --dport 80 -j SNAT --to-source 192.168.6.1 <br/>

## (7) Bibah ingin agar semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop.
Bibah berterima kasih kepada kalian karena telah mau membantunya. Bibah juga mengingatkan agar <br/>
semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan script sebagai backup. <br/>

### Penyelesaian : <br/>
- SURABAYA  <br/>
iptables -N LOGGING <br/>
iptables -A FORWARD -p tcp --dport 22 -d 10.151.73.112/29 -i eth0 -j LOGGING <br/>
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "DROP: " --log-level info <br/>
iptables -A LOGGING -j DROP <br/>

- MALANG <br/>
iptables -N LOGGING <br/>
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j LOGGING <br/>
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "DROP: " --log-level info <br/>
iptables -A LOGGING -j DROP <br/>

- MOJOKERTO <br/>
iptables -N LOGGING <br/>
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j LOGGING <br/>
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "DROP: " --log-level info <br/>
iptables -A LOGGING -j DROP <br/>
