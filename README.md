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

## Nomor 2
Mendrop semua akses HTTP dari luar Topologi pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

## Jawab


## Nomor 3
Membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

## Jawab


## Nomor 4
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

## Jawab


## Nomor 5
Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.

## Jawab


## Nomor 6
Menyetting agar setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate

## Jawab
