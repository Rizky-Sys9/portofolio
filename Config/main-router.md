# Main Router Configuration

## Role & Function
Main Router berfungsi sebagai **gateway utama** yang menghubungkan jaringan internal ke internet.

Fungsi utama:
- Default gateway untuk router distribusi
- NAT (masquerade) ke internet
- Kontrol akses dasar (firewall)
- Monitoring koneksi jaringan

---

## Network Interface
| Interface | Function            |
|---------|---------------------|
| ether1  | WAN / Internet      |
| ether2  | Link to Distribution Router |

---

## IP Addressing
| Interface | IP Address        | Description                  |
|---------|-------------------|------------------------------|
| ether1  | DHCP              | Internet connection          |
| ether2  | trunking          | Point-to-point ke distribusi |
| vlan10  | 10.10.10.1/24     | kepala sekolah               |
| vlan20  | 20.20.20.1/24     | kantor guru                  |
| vlan30  | 30.30.30.1/24     | siswa                        |

---

## IP DHCP-Server

Semua vlan diberikan dhcp-server

---

## Routing
- Default route diarahkan ke ISP
- Route internal didistribusikan melalui router distribusi

## NAT
```bash
/ip firewall nat
add chain=srcnat out-interface=ether1 action=masquerade
