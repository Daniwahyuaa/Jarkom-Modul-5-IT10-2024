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
```
apt-get update
apt-get install isc-dhcp-relay netcat -y
service isc-dhcp-relay start

echo 'SERVERS="192.238.1.10"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=' > /etc/default/isc-dhcp-relay

service isc-dhcp-relay restart
```
2. DHCP Server (Fairy)
```
apt-get update
apt-get install isc-dhcp-server netcat -y

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo 'subnet 192.238.1.64 netmask 255.255.255.192 {
    range 192.238.1.65 192.238.1.125;
    option routers 192.238.1.126;
    option broadcast-address 192.238.1.63;
    option domain-name-servers 192.238.1.9;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 192.238.0.0 netmask 255.255.255.0 {
    range 192.238.0.1 192.238.0.253;
    option routers 192.238.0.254;
    option broadcast-address 192.238.0.255;
    option domain-name-servers 192.238.1.9;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 192.238.1.128 netmask 255.255.255.128 {
    range 192.238.1.129 192.238.1.253;
    option routers 192.238.1.254;
    option broadcast-address 192.238.1.255;
    option domain-name-servers 192.238.1.9;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 192.238.1.8 netmask 255.255.255.248 {
}'> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
3. DNS Server (HDD)
```
apt-get update
apt-get install bind9 netcat -y

echo 'options {
        directory "/var/cache/bind";

        forwarders {
            192.168.122.1;
        };

        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
## Misi 2: Menemukan Jejak Sang Peretas
### No 1
Soal: Agar jaringan di New Eridu bisa terhubung ke luar (internet), kalian perlu mengkonfigurasi routing menggunakan iptables. Namun, kalian tidak diperbolehkan menggunakan MASQUERADE.

Jalankan script berikut sebelum misi 1 no 4 pada router NewEridu agar dapat mengakses internet.
```
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```
### No 2
Soal: Karena Fairy adalah AI yang sangat berharga, kalian perlu memastikan bahwa tidak ada perangkat lain yang bisa melakukan ping ke Fairy. Tapi Fairy tetap dapat mengakses seluruh perangkat.

Jalankan script berikut di dns server Fairy
```
iptables -A OUTPUT -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -j DROP
```
### No 3
Soal: Selain itu, agar kejadian sebelumnya tidak terulang, hanya Fairy yang dapat mengakses HDD. Gunakan nc (netcat) untuk memastikan akses ini. [hapus aturan iptables setelah pengujian selesai agar internet tetap dapat diakses.]

Buat konfigurasi iptables untuk melarang ping dari semua jaringan, lalu tambahkan ip Fairy agar diijinkan ping
```
iptables -A INPUT -s 192.238.1.10 -j ACCEPT
iptables -A INPUT -j DROP
```
### No 3
Soal: Fairy mendeteksi aktivitas mencurigakan di server Hollow. Namun, berdasarkan peraturan polisi New Eridu, Hollow hanya boleh diakses pada hari Senin hingga Jumat dan hanya oleh faksi SoC (Burnice & Caesar) dan PubSec (Jane & Policeboo). Karena hari ini hari Sabtu, mereka harus menunggu hingga hari Senin. Gunakan curl untuk memastikan akses ini.

Jalankan script berikut pada web server HollowZero.
```
iptables -A INPUT -s 192.238.1.64/26 -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 192.238.0.0/24 -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```
### No 5
Soal: Sembari menunggu, Fairy menyarankan Phaethon untuk berlatih di server HIA dan meminta bantuan dari faksi Victoria (Ellen & Lycaon) dan PubSec. Akses HIA hanya diperbolehkan untuk a. Ellen dan Lycaon pada jam 08.00-21.00. b. Jane dan Policeboo pada jam 03.00-23.00. (hak kepolisian) Gunakan Curl untuk memastikan akses ini.
```
iptables -A INPUT -s 192.238.0.0/24 -m time --timestart 03:00 --timestop 23:00 -j ACCEPT
iptables -A INPUT -s 192.238.1.128/25 -m time --timestart 08:00 --timestop 21:00 -j ACCEPT
iptables -A INPUT -j REJECT
```
### No 6
Soal: Sebagai bagian dari pelatihan, PubSec diminta memperketat keamanan jaringan di server HIA. Jane dan Policeboo melakukan simulasi port scan menggunakan nmap pada rentang port 1-100. a. Web server harus memblokir aktivitas scan port yang melebihi 25 port secara otomatis dalam rentang waktu 10 detik. b. Penyerang yang terblokir tidak dapat melakukan ping, nc, atau curl ke HIA. c. Catat log dari iptables untuk keperluan analisis dan dokumentasikan dalam format PDF.

Buat konfigurasi untuk memblokir aktivitas port scanning yang melebihi 25 port dalam rentang 10 detik, penyerang yang diblokir tidak bisa ping, nc, atau curl ke HIA, log dari iptables akan tercatat untuk analisis.
```
iptables -N PORTSCAN

# Mendeteksi aktivitas baru dan menandai IP
iptables -A INPUT -p tcp -m state --state NEW -m recent --set --name portscan

# Blokir IP yang melakukan lebih dari 25 koneksi dalam 10 detik
iptables -A INPUT -p tcp -m state --state NEW -m recent --update --seconds 10 --hitcount 25 --name portscan -j DROP

# untuk melakukan logging
iptables -A INPUT -p tcp -m state --state NEW -m recent --update --seconds 10 --hitcount 25 --name portscan -j LOG --log-prefix "Port Scan Detected: " --log-level 7

#  Blokir ICMP (ping)
iptables -A INPUT -p icmp -m recent --name portscan --rcheck -j DROP

# Blokir TCP dan UDP
iptables -A INPUT -p tcp -m recent --name portscan --rcheck -j DROP
iptables -A INPUT -p udp -m recent --name portscan --rcheck -j DROP

#  Konfigurasi Forward Chain
iptables -A FORWARD -m recent --name portscan --rcheck -j DROP
```
### No 7
Soal: Hari Senin tiba, dan Fairy menyarankan membatasi akses ke server Hollow. Akses ke Hollow hanya boleh berasal dari 2 koneksi aktif dari 2 IP yang berbeda dalam waktu bersamaan. Burnice, Caesar, Jane, dan Policeboo diminta melakukan uji coba menggunakan curl.

Script untuk membuat akses hanya boleh berasal dari 2 koneksi aktif dari 2 ip yang berbeda dalam waktu yang bersamaan pada HollowZero
```
iptables -I INPUT -p tcp --dport 80 -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
iptables -I INPUT -p tcp --dport 443 -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP

iptables -I INPUT -p tcp --dport 80 -m hashlimit --hashlimit-name ip_limit --hashlimit-above 2/sec --hashlimit-mode srcip --hashlimit-srcmask 32 -j DROP
iptables -I INPUT -p tcp --dport 443 -m hashlimit --hashlimit-name ip_limit --hashlimit-above 2/sec --hashlimit-mode srcip --hashlimit-srcmask 32 -j DROP

iptables -I INPUT -p tcp --dport 80 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j DROP
iptables -I INPUT -p tcp --dport 443 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j DROP

iptables -I INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```
### No 8
Soal: Selama uji coba, Fairy mendeteksi aktivitas mencurigakan dari Burnice. Setiap paket yang dikirim Fairy ke Burnice ternyata dialihkan ke HollowZero. Gunakan nc untuk memastikan alur pengalihan ini.
