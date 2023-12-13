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

-`j SNAT`: Menyatakan bahwa _rules_ tersebut adalah Source Network Address Translation.

`--to-source $ETH0_IP`: Menentukan alamat IP sumber untuk melakukan SNAT, menggunakan alamat IP yang telah diperoleh sebelumnya dari eth0.

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

## **Soal Nomor 4**
Coming soon.

## **Penyelesaian Soal Nomor 4**
Coming soon.

# **Kendala Saat Pengerjaan**

- Website DNS tidak bisa diakses dengan jaringan tertentu, seperti wifi kos. Hal tersebut menghambat pengerjaan karena koneksi dari hotspot tidak selalu .stabil.

- Terdapat beberapa soal yang ambigu, sehingga ada perubahan disaat sudah menyelesaikannya.

- Koneksi yang tiba-tiba terputus (_Closed by foreign host_) sehingga menghambat pengerjaan.

# **End of The Line**

```c
#include <stdio.h>

int main(){
    printf("Thank you!");
}
```