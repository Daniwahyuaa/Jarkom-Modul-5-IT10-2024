# Jarkom-Modul-5-IT10-2024

## Anggota Team:

| Nama | NRP                    |
|---------------|---------------------------------|
| Dani Wahyu Anak Ary    | 5027231038 |
| Abid Ubaidillah A      | 5027231089 |

##Prefix IP
Kelompok kami memiliki prefix IP *192.238*

###No 1
Soal: Sebuah topologi sederhana menggambarkan jaringan New Eridu:
![image](https://github.com/user-attachments/assets/39dfed17-cccc-4c1f-9efb-f0f6c6d858ac)
Keterangan: HDD: Berfungsi sebagai DNS Server. Fairy: Berfungsi sebagai DHCP Server. Web Servers: HIA, HollowZero. Client: Burnice: Memiliki 5 host. Lycaon: Memiliki 20 host. Policeboo: Memiliki 30 host. Caesar: Memiliki 50 host Ellen: Memiliki 100 host. Jane: Memiliki 200 host.

Berikut topologi jaringan pada GNS3 seperti yang diberikan soal:
### Topology
![image](https://github.com/user-attachments/assets/9ccd97a3-d7d2-456c-94e0-d217d69fae9f)

No 2
Soal: Setelah membagi alamat IP menggunakan VLSM, gambarkan pohon subnet yang menunjukkan hierarki pembagian IP di jaringan New Eridu. Lingkari subnet-subnet yang akan dilewati dalam jaringan. Berikut adalah tabel routing, tabel pembagian IP VLSM, dan tree VLSM.

#### Tabel Routing:
![image](https://github.com/user-attachments/assets/6fafaab7-04ae-44f2-aa4e-63c0ca666d29)
#### Pembagian IP VLSM:
![image](https://github.com/user-attachments/assets/12815af8-16b6-4451-9093-001c37755275)
#### Tree VLSM:

Untuk topologi jaringan pada GNS3 dengan lingkaran pembagian IP VLSM adalah sebagai berikut.
![PembagianIPIT10](https://github.com/user-attachments/assets/ff1b5eee-7bf9-4e60-8ef7-9dbe63a6f4df)

### No 3

Soal: Setelah pembagian IP selesai, buatlah konfigurasi rute untuk menghubungkan semua subnet dengan benar di jaringan New Eridu. Pastikan perangkat dapat saling terhubung. Sebelum melakukan konfigurasi routing, konfigurasikan network interface tiap node yang ada pada jaringan dengan konfigurasi berikut.

**Router**
NewEridu
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 192.238.1.22
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 192.238.1.34
    netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
ScoutOutpost
```
auto eth0
iface eth0 inet static
    address 192.238.1.1
    netmask 255.255.255.248
    gateway 192.238.1.3

auto eth1
iface eth1 inet static
    address 192.238.1.18
    netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**DHCP Relay
SixStreet
```
auto eth0
iface eth0 inet static
    address 192.238.1.21
    netmask 255.255.255.252
    gateway 192.238.1.22

auto eth1
iface eth1 inet static
    address 192.238.1.3
    netmask 255.255.255.248

auto eth2
iface eth2 inet static
    address 192.238.1.14
    netmask 255.255.255.248

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
OuterRing
```
auto eth0
iface eth0 inet static
    address 192.238.1.2
    netmask 255.255.255.248
    gateway 192.238.1.3

auto eth1
iface eth1 inet static
    address 192.238.1.126
    netmask 255.255.255.192

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
LuminaSquare
```
auto eth0
iface eth0 inet static
    address 192.238.1.33
    netmask 255.255.255.252
    gateway 192.238.1.34

auto eth1
iface eth1 inet static
    address 192.238.1.27
    netmask 255.255.255.248

auto eth2
iface eth2 inet static
    address 192.238.0.254
    netmask 255.255.255.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
BalletTwins
```
auto eth0
iface eth0 inet static
    address 192.238.1.25
    netmask 255.255.255.248
    gateway 192.238.1.27

auto eth1
iface eth1 inet static
    address 192.238.1.254
    netmask 255.255.255.128

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**DNS Server**
```
auto eth0
iface eth0 inet static
    address 192.238.1.9
    netmask 255.255.255.248
    gateway 192.238.1.14

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**DNS Server**
Fairy
```
auto eth0
iface eth0 inet static
    address 192.238.1.10
    netmask 255.255.255.248
    gateway 192.238.1.14

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**Web Server**
HIA
```
auto eth0
iface eth0 inet static
    address 192.238.1.26
    netmask 255.255.255.248
    gateway 192.238.1.27

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
HollowZero
```
auto eth0
iface eth0 inet static
    address 192.238.1.17
    netmask 255.255.255.252
    gateway 192.238.1.18

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**Client**
Caesar, Burnice, Jane, Policeboo, Ellen, Lycaon
```
auto eth0
iface eth0 inet dhcp

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Setelah melakukan konfigurasi network, jalankan command dibawah pada tiap router dan DHCP relay agar antar subnet dapat terhubung.
#### NewEridu
```
post-up route add -net 192.238.1.16 netmask 255.255.255.252 gw 192.238.1.21
post-up route add -net 192.238.1.64 netmask 255.255.255.192 gw 192.238.1.21
post-up route add -net 192.238.1.0 netmask 255.255.255.248 gw 192.238.1.21
post-up route add -net 192.238.1.8 netmask 255.255.255.248 gw 192.238.1.21
post-up route add -net 192.238.1.128 netmask 255.255.255.128 gw 192.238.1.33
post-up route add -net 192.238.1.24 netmask 255.255.255.248 gw 192.238.1.33
post-up route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.33
```
#### SixStreet
```
post-up route add -net 192.238.1.16 netmask 255.255.255.252 gw 192.238.1.1
post-up route add -net 192.238.1.64 netmask 255.255.255.192 gw 192.238.1.2
```
#### ScoutOutpost, OuterRing
```
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.79.1.3
```
#### LuminaSquare
```
post-up route add -net 192.238.1.128 netmask 255.255.255.128 gw 192.238.1.25
```
#### BalletTwins
```
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.238.1.27
```
### No 4
Soal: Konfigurasi → dikerjakan setelah misi 2 nomor 1

-Fairy sebagai DHCP Server agar perangkat yang berada dalam Burnice, Caesar, Ellen, Jane, Lycaon, dan Policeboo dapat menerima alamat IP secara otomatis.
-OuterRing, BalletTwins, Sixstreet dan LuminaSquare Sebagai DHCP Relay
-HDD sebagai DNS server
-HIA dan HollowZero Sebagai Web server (gunakan apache) index.html
```
Welcome to {hostname}
```
### Script Konfigurasi
1. DHCP Relay (OuterRing, SixStreet, LuminaSquare, BalletTwins)
