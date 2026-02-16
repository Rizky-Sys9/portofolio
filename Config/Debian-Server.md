# Debian Server 

## Role and Function 
Debian server berfungsi sebagai media webserver dan database (jika deperlukan).

Fungsi utama server:
- Web Server (Apache2)
- DNS Server (Bind9)
- DHCP Server
- Firewall (UFW / iptables)
- Media penyimpanan konfigurasi & backup
- Database Server (opsional, jika diperlukan)

Server ditempatkan pada jaringan internal dan **tidak diekspos langsung ke internet** untuk menjaga keamanan.

---

## Operating System
- OS: Debian GNU/Linux
- Version: (isi versi Debian yang kamu pakai)
- Access: SSH (key-based / password)

---

## Server Network Design
Debian server ditempatkan pada subnet terpisah yang terhubung langsung ke main router.

- Server network menggunakan interface ether3 pada main router
- Server tidak berada dalam VLAN user
- Akses ke server dilakukan melalui routing antar subnet
- Tidak ada port forwarding dari internet ke server

Desain ini bertujuan untuk:
- Memisahkan server dan user network
- Meningkatkan keamanan
- Memudahkan kontrol akses layanan