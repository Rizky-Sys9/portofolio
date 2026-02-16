# Distribusi Router Configuration

## Role and Function 
Distribusi router berfungsi untuk menerima ip dari main router dan disalurkan ke client sesuai dengan vlan yang sudah tersedia.

---

## Network Interface
| Interface | Function|
|-----------|---------|
| Ether1     | Link to main router|
| Ether2    | vlan10  |
| Ether3    | Vlan20  |
| Ether4    | Vlan 30 | 

## Bridge configuration 

## Bridge Configuration
Bridge digunakan untuk mengelola lalu lintas VLAN dari access switch ke router distribusi melalui satu interface logis.

Tujuan penggunaan bridge:
- Menyederhanakan manajemen VLAN
- Mendukung trunk VLAN ke access switch
- Mempermudah penambahan VLAN baru di masa depan

---

## Bridge Setup
Bridge dibuat sebagai interface utama untuk VLAN trunk.

```bash
/interface bridge
add name=bridge1 protocol-mode=none vlan-filtering=yes

/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2 pvid=10
add bridge=bridge1 interface=ether3 pvid=20
add bridge=bridge1 interface=ether4 pvid=30
add bridge=bridge1 interface=vlan10 pvid=10
add bridge=bridge1 interface=vlan20 pvid=20
add bridge=bridge1 interface=vlan30 pvid=30

/interface bridge vlan
add bridge=bridge1 vlan-ids=10 tagged=bridge1,ether2
add bridge=bridge1 vlan-ids=20 tagged=bridge1,ether2
add bridge=bridge1 vlan-ids=30 tagged=bridge1,ether2

/interface vlan
add name=vlan10-kepsek vlan-id=10 interface=bridge1
add name=vlan20-guru vlan-id=20 interface=bridge1
add name=vlan30-siswa vlan-id=30 interface=bridge1
