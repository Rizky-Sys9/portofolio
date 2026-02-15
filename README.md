# Network Infrastructure Simulation - School / Office Enviroment 

## Overview
Project ini merupakan simulasi infrastruktur jaringan kantor/sekolah menggunakan **GNS3** dengan pendekatan **Hierarchical Network Design**.
Tujuan utama project ini adalah memahami perancangan jaringan tersegmentasi, routing antar VLAN, serta intergrasi server terpusat berbasis Linux (Debian).

---

## Network Topologi 
Topologi jaringan dibagi menjadi beberapa layer : 

- **Main Router**
  - Berfungsi sebagai gateway utama menuju internet
  - Menangani koneksi keluar (NAT)

- **Distribusi Router**
  - Mengelola routing antar VLAN
  - Menghubungkan access switch ke main router

- **Access Switch**
  - Menghubungkan end device (client) 
  - Menerapkan segmentasi VLAN

- **Debian Server**
  - Server terpusat untuk layanan jaringan 
  - Terpisah dari jaringan client 

  ---

## VLAN Design
Segmentasi jaringan menggunakan VLAN untuk meningkatkan keamanan dan manajemen jaringan:

| VLAN ID | Nama Jaringan        | Pengguna            |
|-------|----------------------|-----------------------|
| 10    | Kepala Sekolah       | User (End Device)     |
| 20    | Kantor Guru          | User (Staff / Guru)   |
| 30    | Siswa                | User (Client Umum)    |

Manfaat VLAN:
- Mengurangi broadcast
- Meningkatkan keamanan
- Mempermudah manajemen jaringan

---

## IP Addressing
- Setiap VLAN memiliki subnet tersendiri
- Gateway ditentukan pada router distribusi
- Client mendapatkan IP sesuai VLAN masing-masing

---

## Routing
- Inter-VLAN routing dikonfigurasi pada **router distribusi**
- Default route diarahkan ke **main router**
- Akses internet dilakukan melalui NAT

---

## Server Configuration (Debian)
Server Debian dikonfigurasi sebagai server terpusat dengan layanan berikut:

- DHCP Server
- DNS Server (Bind9)
- Web Server (Apache2)
- Firewall (iptables / UFW)

Server ditempatkan pada jaringan terpisah untuk meningkatkan keamanan dan stabilitas.

---

## Backup & Recovery
Konfigurasi server dibackup menggunakan `tar` dan disimpan di media terpisah.

Contoh backup:
```bash
tar czvf backup-config-YYYY-MM-DD.tar.gz \
/etc \
/etc/apache2 \
/etc/bind \
/var/www/html \
/var/lib/dhcp
