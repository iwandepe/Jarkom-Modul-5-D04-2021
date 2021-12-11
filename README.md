# Jarkom-Modul-5-D04-2021

1. Daffa Muhamad Azhar [05111940000037]
2. Taqarra Rayhan I [05111940000121]
3. Iwan Dwi Prakoso [05111940000229]

# MODUL 5
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
