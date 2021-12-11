# Jarkom-Modul-5-D04-2021

1. Daffa Muhamad Azhar [05111940000037]
2. Taqarra Rayhan I [05111940000121]
3. Iwan Dwi Prakoso [05111940000229]

# MODUL 5
## Konfigurasi
### A. Membuat Topologi

Topologi dibuat sama seperti soal

![topologi.PNG](https://github.com/iwandepe/Jarkom-Modul-5-D04-2021/blob/main/img/topologi.PNG)

### B. Lakukan Subnetting dengan CIDR atau VLSM
untuk kali ini kami menggunakan CIDR

untuk perhitungannya dapat dilihat pada link berikut :
[CIDR - MODUL 5](https://docs.google.com/spreadsheets/d/10G5YkF7jbdOyspjlx13iXkpxb9JRhdjOuVxj7IeMbXg/edit?usp=sharing)

### C. Lakukan Routing agar semua terhubung
untuk cara melakukan routing sama seperti pada modul 4

untuk link modul 4 sendiri bisa diakses di:

[MODUL 4 - D04](https://github.com/azhar416/Jarkom-Modul-4-D04-2021)

### D. memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

setiap ip client diubah dari static menjadi dhcp. dan pada setiap router diinstall juga dhcp relay yg mengarah ke dhcp server (JIPANGU).

## Nomor 1 
Agar topologi dapat mengakses keluar, konfigurasi Foosha menggunakan iptables, tetapi tidak menggunakan MASQUERADE.

## Jawab
menjalakan `iptables -t nat -A POSTROUTING -s 10.23.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.7` pada foosha lalu untuk testing dapat dicoba dengan ngeping google pada node lain
![no1](#)

-t nat: Menggunakan tabel NAT karena akan mengubah alamat asal dari paket
-A POSTROUTING: Menggunakan chain POSTROUTING karena mengubah asal paket setelah routing
-s 10.23.0.0/20: Mendifinisikan alamat asal dari paket yaitu semua alamat IP dari subnet 10.23.0.0/20
-o eth0: Paket keluar dari eth0 Foosha
-j SNAT: Menggunakan target SNAT untuk mengubah source atau alamat asal dari paket
-to-source 192.168.122.7: Mendefinisikan IP source, di mana digunakan eth0 Foosha 

kemudian dapat ping pada node lain seperti water7
![no1.1](#)



## Nomor 2
Mendrop semua akses HTTP dari luar Topologi pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

## Jawab
jalankan command `iptables -A FORWARD -d 10.23.4.128/29 -i eth0 -p tcp --dport 80 -j DROP` pada foosha

Keterangan
-A FORWARD: Menggunakan chain FORWARD
-p tcp: Mendefinisikan protokol yang digunakan, yaitu tcp
--dport 80: Mendefinisikan port yang digunakan, yaitu 80 (HTTP)
-d 10.23.4.128/29: Mendefinisikan alamat tujuan dari paket (DHCP dan DNS SERVER ) berada pada subnet 10.23.4.128/29
-i eth0: Paket masuk dari eth0 Foosha
-j DROP: Paket di-drop

untuk melakukan testing dapat melakukan hal  berikut
pertama install etcat di server Jipangu dan Doriki: `apt-get install netcat`. Pada Jipangu dan Doriki ketikkan ` nc -l -p 80`
kemudian pada foosha ketikkan `nmap -p 80 10.23.4.131 `atau `nmap -p 80 10.23.4.130`.

![no2](#)

![no2.1](#)


## Nomor 3
Membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

## Jawab
menjalankan  command 
`
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP

`
pada jipangu dan doriki, untuk testing dapat dicoba dengan ping ke arah jipangu atau doriki dari 4 node yang berbeda, maka nanti pada node 4 respon akan berhenti

## Nomor 4
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

## Jawab
untuk membatasi blueno dapat menggunakan command berikut
`
iptables -A INPUT -s 10.23.4.0/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 10.23.4.0/25 -j REJECT

`

untuk membatasi klien cipher dapat menjalan command berikut
`sh
iptables -A INPUT -s 10.23.0.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 10.23.0.0/22 -j REJECT
`


## Nomor 5
Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.

## Jawab
untuk klien elena dapat melakukan command berikut 
`

iptables -A INPUT -s 10.23.10.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT

`

dan untuk klien fukuro dapat seperti berikut 
`sh
iptables -A INPUT -s 10.23.8.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT

`

## Nomor 6
Menyetting agar setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate

## Jawab


`
echo 'zone "jarkomd04.com" {
        type master;
        file "/etc/bind/jarkom/jarkomd04.com";
};'>> /etc/bind/named.conf
`

