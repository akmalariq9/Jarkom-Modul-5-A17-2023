# **Praktikum 5 Jaringan Komputer**
<div align=justify>

Berikut adalah Repository dari Kelompok A17 untuk pengerjaan Praktikum Modul 5 Jaringan Komputer. Dalam Repository ini terdapat Anggota Kelompok, Dokumentasi serta Penjelasan tiap soal, Screenshot Output, dan Kendala yang dialami.

# **Anggota Kelompok**

| Nama                      | NRP        | Kelas                |
| ------------------------- | ---------- | ----------------     |
| Andrian                   | 5025211079 | Jaringan Komputer A  |
| Akmal Ariq Romadhon       | 5025211188 | Jaringan Komputer A  |


# **Dokumentasi dan Penjelasan Soal**
<div align=justify>

Berikut adalah dokumentasi yang berisi source code dari tiap soal dan penjelasan terkait perintah, _command_, syntax, dan _rules_ yang digunakan. 

## **Soal Nomor 0**
Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

- Tugas pertama, buatlah peta wilayah sesuai berikut ini:

![soal](https://cdn.discordapp.com/attachments/1150687865420906517/1184484791542886420/image.png?ex=658c246c&is=6579af6c&hm=2b732fcbdf3cff73978076caf17f3e1780f3b56da9da434369ccfc74b700be48&)

- Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati.

- Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan. 

- Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.


## **Penyelesaian Soal Nomor 0**
Setelah topologi berhasil dibuat pada GNS3, langkah selanjutnya yang dilakukan adalah membuat rute dan melakukan _subnetting_. Berikut adalah hasil dari pembuatan rute serta _subnetting_ yang sudah dilakukan:

- **Tree**

![Tree](https://cdn.discordapp.com/attachments/1150687865420906517/1184487535808892990/tree.png?ex=658c26fb&is=6579b1fb&hm=116392795ce6874371c54612d6849d888db084851c6dc6f7fb111c02d914accb&)

- **Rute**

![Tree](https://media.discordapp.net/attachments/1150687865420906517/1184487979490750494/image.png?ex=658c2765&is=6579b265&hm=ac8ad514bf43abb7d3c2413cdf37cb5c8505276ac2d3cd1aa2282b1a79d1b871&=&format=webp&quality=lossless&width=1016&height=392)

Dokumentasi lengkap untuk rute dan _subnetting_ (termasuk pembagian IP untuk tiap node) dapat diakses [disini](https://its.id/m/Subnetting-A17) atau melalui link berikut: https://its.id/m/Subnetting-A17. 

- **Kongfigurasi setiap _node_** <br>

Setelah melakukan _subnetting_, maka langkah selanjutnya adalah melakukan kongfigurasi untuk setiap node. Berikut adalah kongfigurasi untuk tiap node dalam topologi pada soal praktikum:

- Aura

```shell
auto eth0
iface eth0 inet dhcp
# up iptables -t nat -A POSTROUTING -o eth0 -j SNAT

#A8
# Static config for eth1
auto eth1
iface eth1 inet static
        address 192.177.0.21
        netmask 255.255.255.252
#       up echo nameserver 192.168.1.1 > /etc/resolv.conf

#A6
# Static config for eth2
auto eth2
iface eth2 inet static
        address 192.177.0.13
        netmask 255.255.255.252
#       up echo nameserver 192.168.2.1 > /etc/resolv.conf

#ForHeiter
up route add -net 192.177.4.0 netmask 255.255.252.0 gw 192.177.0.22
up route add -net 192.177.8.0 netmask 255.255.248.0 gw 192.177.0.22

#ForFrieren
up route add -net 192.177.0.0 netmask 255.255.255.252 gw 192.177.0.14
up route add -net 192.177.0.4 netmask 255.255.255.252 gw 192.177.0.14
up route add -net 192.177.2.0 netmask 255.255.254.0 gw 192.177.0.14
up route add -net 192.177.0.128 netmask 255.255.255.128 gw 192.177.0.14
up route add -net 192.177.0.16 netmask 255.255.255.252 gw 192.177.0.14
up route add -net 192.177.0.8 netmask 255.255.255.252 gw 192.177.0.14
```

- **Revolte**
```bash
#A1
auto eth0
iface eth0 inet static
        address 192.177.0.2
        netmask 255.255.255.252
        gateway 192.177.0.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Richter**
```bash
#A2
auto eth0
iface eth0 inet static
	address 192.177.0.6
	netmask 255.255.255.252
	gateway 192.177.0.5
        up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Fern**
```bash
#A3
auto eth0
iface eth0 inet static
	address 192.177.0.130
	netmask 255.255.255.128
	gateway 192.177.0.129

#A2
auto eth1
iface eth1 inet static
	address 192.177.0.5
	netmask 255.255.255.252
#	gateway 192.168.1.1
#	up echo nameserver 192.168.1.1 > /etc/resolv.conf

#A1
auto eth2
iface eth2 inet static
	address 192.177.0.1
	netmask 255.255.255.252
#	gateway 192.168.2.1
#	up echo nameserver 192.168.2.1 > /etc/resolv.conf

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **SchwerMountain**
```bash
#A3
auto eth0
iface eth0 inet dhcp
# iface eth0 inet static
#	address 192.177.0.131
#	netmask 255.255.255.128
	gateway 192.177.0.129

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Himmels**
```bash
#A5
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.177.0.10
	netmask 255.255.255.252
	gateway 192.177.0.9
#	up echo nameserver 192.168.0.1 > /etc/resolv.conf

#A4
# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.177.2.1
	netmask 255.255.254.0
#	gateway 192.177.0.9
#	up echo nameserver 192.168.1.1 > /etc/resolv.conf

#A3
# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.177.0.129
	netmask 255.255.255.128
#	gateway 192.177.0.9
#	up echo nameserver 192.168.2.1 > /etc/resolv.conf

up echo nameserver 192.168.122.1 > /etc/resolv.conf

up route add -net 192.177.0.0 netmask 255.255.255.252 gw 192.177.0.130
up route add -net 192.177.0.4 netmask 255.255.255.252 gw 192.177.0.130
```

- **LaubHills**
```bash
#A4
# Static config for eth0
auto eth0
iface eth0 inet dhcp
# iface eth0 inet static
#	address 192.177.2.2
#	netmask 255.255.254.0
	gateway 192.177.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Frieren**
```bash
#A6
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.177.0.14
	netmask 255.255.255.252
	gateway 192.177.0.13
#	up echo nameserver 192.168.0.1 > /etc/resolv.conf

#A7
# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.177.0.17
	netmask 255.255.255.252
#	gateway 192.177.0.13
#	up echo nameserver 192.168.1.1 > /etc/resolv.conf

#A5
# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.177.0.9
	netmask 255.255.255.252
#	gateway 192.177.0.13
#	up echo nameserver 192.168.2.1 > /etc/resolv.conf

up echo nameserver 192.168.122.1 > /etc/resolv.conf

up route add -net 192.177.0.0 netmask 255.255.255.252 gw 192.177.0.10
up route add -net 192.177.0.4 netmask 255.255.255.252 gw 192.177.0.10
up route add -net 192.177.2.0 netmask 255.255.254.0 gw 192.177.0.10
up route add -net 192.177.0.128 netmask 255.255.255.128 gw 192.177.0.10
```

- **Stark**
```bash
#A7
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.177.0.18
	netmask 255.255.255.252
	gateway 192.177.0.17
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Heiter**
```bash
#A8
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.177.0.22
	netmask 255.255.255.252
	gateway 192.177.0.21
#	up echo nameserver 192.168.0.1 > /etc/resolv.conf

#A9
# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.177.8.1
	netmask 255.255.248.0 
#	gateway 192.177.0.21
#	up echo nameserver 192.168.1.1 > /etc/resolv.conf

#A10
# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.177.4.1
	netmask 255.255.252.0 
#	gateway 192.177.0.21
#	up echo nameserver 192.168.2.1 > /etc/resolv.conf

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **TurkRegion**
```bash
#A9
auto eth0
iface eth0 inet dhcp
# iface eth0 inet static
#	address 192.177.8.2
#	netmask 255.255.248.0 
	gateway 192.177.8.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **Sein**
```bash
#A10
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.177.4.2
	netmask 255.255.252.0 
	gateway 192.177.4.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- **GrobeForest**
```bash
#A10
auto eth0
iface eth0 inet dhcp
# iface eth0 inet static
#	address 192.177.4.3
#	netmask 255.255.252.0 
	gateway 192.177.4.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

Kemudian, dilakuka kongfigurasi untuk _set-up_ DHCP di beberapa node seperti berikut:

- **Revolte** - dhcpd.conf

```bash
#A1
subnet 192.177.0.0 netmask 255.255.255.252 {
}

#A2
subnet 192.177.0.4 netmask 255.255.255.252 {
}

#A3
subnet 192.177.0.128 netmask 255.255.255.128 {
    range 192.177.0.131 192.177.0.254;
    option routers 192.177.0.129;
    option broadcast-address 192.177.0.255;
    default-lease-time 180;
    max-lease-time 5760;
}

#A4
subnet 192.177.2.0 netmask 255.255.254.0 {
    range 192.177.2.2 192.177.2.254;
    option routers 192.177.2.1;
    option broadcast-address 192.177.2.255;
    default-lease-time 180;
    max-lease-time 5760;
}

#A5
subnet 192.177.0.8 netmask 255.255.255.252 {
}

#A6
subnet 192.177.0.12 netmask 255.255.255.252 {
}

#A7
subnet 192.177.0.16 netmask 255.255.255.252 {
}

#A8
subnet 192.177.0.20 netmask 255.255.255.252 {
}

#A9
subnet 192.177.8.0 netmask 255.255.248.0 {
    range 192.177.8.2 192.177.15.254;
    option routers 192.177.8.1;
    option broadcast-address 192.177.15.255;
    default-lease-time 180;
    max-lease-time 5760;
}

#A10
subnet 192.177.4.0 netmask 255.255.252.0 {
    range 192.177.4.3 192.177.7.254;
    option routers 192.177.4.1;
    option broadcast-address 192.177.7.255;
    default-lease-time 180;
    max-lease-time 5760;
}
```

- **DHCP Relay** - isc-dhcp-relay
```bash
SERVERS="192.177.0.2"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

## **Soal Nomor 1**
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## **Penyelesaian Soal Nomor 1**
Untuk membuat Aura dan _node_ lain dapat terhubung ke internet tanpa menggunakan Masquerade, maka digunakan _syntax_ berikut:

```bash
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```

Berikut adalah penjelasan dari _syntax_ tersebut beserta masing-masing fungsinya:

`ip -4 addr show eth0:` Menampilkan informasi alamat IP untuk antarmuka jaringan eth0.

`grep -oP '(?<=inet\s)\d+(\.\d+){3}'`: Menggunakan grep untuk mengambil alamat IP dari baris yang mengandung "inet" pada output sebelumnya.`

`iptables -t nat -A POSTROUTING`: Menambahkan aturan ke chain POSTROUTING pada tabel nat.

`-o eth0`: Menentukan antarmuka keluar (outgoing) sebagai eth0.

`-j SNAT`: Menyatakan bahwa _rules_ tersebut adalah Source Network Address Translation.

`--to-source $ETH0_IP`: Menentukan alamat IP sumber untuk melakukan SNAT, menggunakan alamat IP yang telah diperoleh sebelumnya dari eth0.

_Output_ dari nomor 1 adalah tiap _route_ dapat melakukan ping keluar (misalnya: google.com) seperti pada gambar berikut:

![ping](https://cdn.discordapp.com/attachments/1150687865420906517/1184517860035416174/image.png?ex=658c4339&is=6579ce39&hm=fb9ba71f60f1c18ae11f2d3ad1631e2ca8cab324bc853b3dd069c3b468767067&)

![ping2](https://cdn.discordapp.com/attachments/1150687865420906517/1184518049404030996/image.png?ex=658c4366&is=6579ce66&hm=bc9b359d8f8557f9f5012fd672e12b2ad90abce29f61146b275e001f96894abe&)

## **Soal Nomor 2**
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

## **Penyelesaian Soal Nomor 2**
Untuk menyelesaikan soal nomor 2, maka diperlukan stntax berikut:

```bash
iptables -F

iptables -A INPUT -p icmp -j ACCEPT

iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

iptables -A INPUT -p tcp -j DROP

iptables -A INPUT -p udp -j DROP
```

Dari _syntax_ tersebut dapat dilihat bahwa _node_ tersebut hanya menerima koneksi dari port 8080 dengan koneksi TCP. Berikut adalah hasil _testing_ yang sudah dilakukan:

- _Syntax_ untuk membuka koneksi dari _client_:

![syntax](https://cdn.discordapp.com/attachments/1150687865420906517/1184184840510259262/image.png?ex=658b0d13&is=65789813&hm=e93d36c5a8f1ffdd9c1ab382fd8682b218041eed143904d06346d8beaa1ed969&)

- _Testing_ dengan port 8080 dan 8000

![Testing](https://cdn.discordapp.com/attachments/1150687865420906517/1184184881148866641/image.png?ex=658b0d1c&is=6578981c&hm=8b53ac6c1c5d4beb525cf0aa05589b1023f496eb86aedcf10ec93ae89a1bb6f0&)

![testing2](https://cdn.discordapp.com/attachments/1150687865420906517/1184184913591799808/image.png?ex=658b0d24&is=65789824&hm=2b051f562b7b55d08e14fc3bcd4bf3037d066bea18604f2fdff5b8ebe5671057&)

## **Soal Nomor 3**
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

## **Penyelesaian Soal Nomor 3**

Untuk menyelesaikan soal nomor 3 dapat digunakan _syntax_ berikut:
```bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

Kemudian dilakukan _testing_ dengan cara melakukan ping menuju _node_ tersebut dengan 4 _node_. Berikut adalah hasil testing yang telah dilakukan:

![nomor4](https://cdn.discordapp.com/attachments/1150687865420906517/1184193453404454973/image.png?ex=658b1518&is=6578a018&hm=3c7a9d1771330a1a545aca6fc1c170ea59c6f145550d1cae0d57bce6ae8ad99e&)

Dapat dilihat bahwa _node_ keempat yang melakukan ping akan gagal dan tidak bisa tersambung dengan _node_ tujuan.

## **Soal Nomor 4**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

## **Penyelesaian Soal Nomor 4**
Untuk menyelesaikan soal nomor 4, dapat digunakan _syntax_ berikut:

```bash
iptables -A INPUT -p tcp --dport 22 -s 192.177.4.0/22 -j ACCEPT

iptables -A INPUT -p tcp --dport 22 -j DROP
```

Dalam _syntax_ tersebut dilakukan pembatasan untuk subnet dari GrobeForest, serta hanya bisa diakses oleh ip 22 atau SSH. Berikut adalah hasil _testing_ untuk nomor 4:

![nomor4](https://cdn.discordapp.com/attachments/1150687865420906517/1184203176174424104/image.png?ex=658b1e26&is=6578a926&hm=48ee1ecbf1dabf27c4722849d90513001495b3e43ddb48d8a21dc19457b54377&)

Dapat dilihat bahwa untuk _GrobeForest_ menunjukkan hasil _open_, sedangkan untuk _node_ lain _filtered_ atau tidak berhasil

## **Soal Nomor 5**
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

## **Penyelesaian Soal Nomor 5**
Nomor 5 dapat diselesaikan dengan menambahkan _rules_ pada iptables menggnakan _syntax_ berikut:

```bash
iptables -A INPUT -p tcp --dport 22 -s 192.177.4.0/22 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -p tcp --dport 22 -j DROP
```

_Testing_ dapat dilakukan dengan merubah tanggal pada node lalu melakukan koneksi menuju tujuan dengan nmap. Berikut adalah hasil _testing_ untuk _rules_ tersebut:

![Success](https://cdn.discordapp.com/attachments/1150687865420906517/1184206395676037130/image.png?ex=658b2126&is=6578ac26&hm=9be8023b30389e36cee6819554229fb2d4d4d2dd777d6e573e78b6c1ff39e7ef&)

![Fail](https://cdn.discordapp.com/attachments/1150687865420906517/1184208186237005824/image.png?ex=658b22d1&is=6578add1&hm=7f2dd0bf6a6b49c83c99b920d1c33adad5185bd43019f114384af831b2965cef&)

Dapat dilihat pada gambar pertama sebelah kiri menunjukkan hasil sukses, karena _webserver_ diakses oleh GrobeForest dengan _date_ yang sesuai. Sedangkan pada gambar bawah sebelah kiri menunjukkan _fail_ karena _date_ nya tidak sesuai. 

## **Soal Nomor 6**
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## **Penyelesaian Soal Nomor 6**
Nomor 6 dapat diselesaikan dengan menambahkan _rules_ setelah nomer 5 menggunakan _syntax_ berikut:

```bash
iptables -A INPUT -p tcp --dport 22 -s 192.177.4.0/22 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP

iptables -A INPUT -p tcp --dport 22 -s 192.177.4.0/22 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
```

_Testing_ dapat dilakukan dengan merubah _date_ dari _node_ lain lalu `nmap` ke _webserver_. Berikut adalah hasil _testing_ yang telah dilakukan:

![nomor6](https://cdn.discordapp.com/attachments/1150687865420906517/1184210886597034074/image.png?ex=658b2554&is=6578b054&hm=7089bfb6cac9cae2083d734834bea4873bc8c4f5e8c95a076720bbf71d20f767&)

## **Soal Nomor 7**
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## **Penyelesaian Soal Nomor 7**
Soal nomor 7 dapat diseleseaika dengan mengaktifkan _rules_ pada iptables di _router_ yang terhubung dengan _webserver_, salah satunya adalah heiter. Berikut adalah _syntax_ yang digunakan untuk menyelesaikan nomor 7:
```bash
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 192.177.4.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.177.4.2

iptables -A PREROUTING -t nat -p tcp --dport 80 -d 192.177.4.2 -j DNAT --to-destination 192.177.0.18

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 192.177.0.18 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.177.0.18

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 192.177.0.18 -j DNAT --to-destination 192.177.4.2
```
Kemudian dapat dilakukan testing dengan cara membuka koneksi pada _webserver_ yaitu sein dan stark dengan syntax berikut untuk port 80 `while true; do nc -l -p 80 -c 'echo "ini sein"'; done` dan `while true; do nc -l -p 443 -c 'echo "ini stark"'; done`. 

Sedangkan untuk port 443 dapat menggunakan _syntax `while true; do nc -l -p 443 -c 'echo "ini sein"'; done` dan 
`while true; do nc -l -p 443 -c 'echo "ini stark"'; done`. Berikut adalah hasil testing yang dilakukan:

![nomor7-80](https://cdn.discordapp.com/attachments/1150687865420906517/1184479918403371008/image.png?ex=658c1fe3&is=6579aae3&hm=8dd626a13850931ca8b937bb1a37b1dfd672065a407f0440848632afb26ed583&)

![nomor7-443](https://cdn.discordapp.com/attachments/1150687865420906517/1184480387922133052/image.png?ex=658c2053&is=6579ab53&hm=78430ddc12f627d5ad48778dee8135f0033d3f5462fc73d0a85e3e87adcdb998&)

Dapat dilihat bahwa ketika terdapat _node_ yang mengakses _webserver_, akan muncul log atau pesan bahwa sein dan stark telah bekerja secara bergantian

## **Soal Nomor 8**
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## **Penyelesaian Soal Nomor 8**
Nomor 8 dapat diselesaikan dengan menambahkan _rules_ pada _webserver_ menggunakan _syntax_ berikut:
```bash
Revolte_Subnet="192.177.0.0/30"

Pemilu_Start=$(date -d "2023-10-19T00:00" +"%Y-%m-%dT%H:%M")

Pemilu_End=$(date -d "2024-02-15T00:00" +"%Y-%m-%dT%H:%M")

# Atur waktu untuk masa pemilu
iptables -A INPUT -p tcp -s $Revolte_Subnet --dport 80 -m time --datestart "$Pemilu_Start" --datestop "$Pemilu_End" -j DROP
``` 

Untuk melakukan _testing_ nomor 8 dapat dilakukan dengan merubah _date_ sesuai yang diminta pada soal. Berikut adalah hasil _testing_ dari _syntax_ tersebut:

![nomor8](https://cdn.discordapp.com/attachments/1150687865420906517/1184413983571185664/image.png?ex=658be27b&is=65796d7b&hm=335852333b753f44456bc55c5705ea2480ed08b0f4c3379210c75095b82767ee&)

Dapat dilihat bahwa Revolte _fail_ saat mengakses _webserver_ sedangkan GrobeForest berhasil disaat tanggal telah diatur berada pada masa pemilu.

## **Soal Nomor 9**
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)

## **Penyelesaian Soal Nomor 9**
_Coming soon_.

## **Soal Nomor 10**
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 

## **Penyelesaian Soal Nomor 10**
Untuk menyelesaikan soal nomor 10 dapat digunakan _syntax_ berikut:

```bash
iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet' -m limit --limit 1/second --limit-burst 10
```

Berikut adalah penjelasan dari bagian pada _syntax_ tersebut:

`-A INPUT`: Menambahkan aturan ke chain INPUT.

`-j LOG`: Menunjukkan bahwa aksi yang akan diambil adalah log. Ketika paket mencocokkan aturan ini dan ditolak, informasi tentang paket tersebut akan dicatat dalam log sistem.

`--log-level debug`: Menentukan level log yang akan digunakan. Dalam hal ini, level log adalah "debug", yang berarti log akan mencatat informasi lebih rinci.

`--log-prefix 'Dropped Packet'`: Menetapkan prefix atau awalan untuk setiap entri log. Dalam hal ini, pesan log akan dimulai dengan teks "Dropped Packet".

`-m limit --limit 1/second --limit-burst 10`: Menggunakan modul "limit" untuk mengatur batasan pada jumlah log yang akan dicatat.

`--limit 1/second`: Menetapkan batasan sebanyak satu log per detik.

`--limit-burst 10`: Menetapkan batasan burst, yaitu jumlah log yang dapat dilakukan dalam satu waktu sebelum batasan per detik diambil kembali.

Berikut adalah hasil dari _syntax_ yang dijalankan, sehingga terdapat _rules_ untuk membuat _log_ sehingga dapat dilihat paket yang telah didrop.

![nomor10](https://cdn.discordapp.com/attachments/1150687865420906517/1184516962756345866/image.png?ex=658c4263&is=6579cd63&hm=a5304fc99143c9b10442ec99d7bf09a80f5176830b9767251006e570b8838bff&)

# **Kendala Saat Pengerjaan**

- Ketidaktelitian saat membuat _tree_ dan _subnetting_ sehingga banyak terjadi kegagalan saat melakukan kongfigurasi di GNS3.

- _Bug_ atau _error_ pada netcat dan nmap yang membuat output tidak muncul meski _syntax_ yang dijalankan sudah benar.

- Koneksi yang tiba-tiba terputus (_Closed by foreign host_) sehingga menghambat pengerjaan.

# **End of The Line**

```c
#include <stdio.h>

int main(){
    printf("Thank you!");
}
```