# Langkah Konfigurasi MikroTik dan Starlink

## Deskripsi

Dokumentasi ini berisi langkah-langkah konfigurasi MikroTik pada implementasi jaringan internet berbasis Starlink. Konfigurasi dilakukan untuk mengatur distribusi koneksi internet dari Starlink menuju pengguna melalui perangkat MikroTik dan Access Point.

## 1. Persiapan Perangkat

Perangkat yang digunakan dalam implementasi jaringan terdiri dari:

- Starlink sebagai sumber koneksi internet.
- Router MikroTik sebagai perangkat manajemen jaringan.
- Access Point sebagai perangkat distribusi jaringan kepada pengguna.
- Kabel LAN/Fiber Optic sebagai media transmisi jaringan.
- Laptop/PC untuk melakukan konfigurasi menggunakan aplikasi WinBox.

---

# 2. Topologi Jaringan

Implementasi jaringan menggunakan Starlink sebagai sumber koneksi internet yang terhubung ke router MikroTik. MikroTik berfungsi sebagai perangkat pengelola jaringan yang melakukan konfigurasi alamat IP, distribusi koneksi internet, serta pengaturan layanan Hotspot kepada pengguna melalui Access Point.

![Topologi Jaringan](/images/01-topologi.jpg)

---

# 3. Konfigurasi MikroTik

Tahapan konfigurasi MikroTik pada implementasi jaringan Starlink meliputi:

1. Konfigurasi Interface MikroTik
2. Konfigurasi Bridge Hotspot
3. Konfigurasi DHCP Client
4. Konfigurasi IP Address
5. Konfigurasi DHCP Server untuk Jaringan Hotspot
7. Aktivasi DHCP Server pada Jaringan Hotspot
8. Konfigurasi NAT (Network Address Translation)
9. Konfigurasi Hotspot MikroTik
10. Konfigurasi User Profile dan User Hotspot
11. Pengujian Koneksi Jaringan

---

# 3.1 Konfigurasi Interface MikroTik

Konfigurasi interface dilakukan untuk menentukan fungsi setiap port pada MikroTik. Interface yang digunakan disesuaikan dengan kebutuhan jaringan, yaitu koneksi dari Starlink dan jaringan distribusi menuju pengguna.

![Konfigurasi Interface MikroTik](/images/02-interface.jpg)

---

# 3.2 Konfigurasi Bridge Hotspot

Bridge digunakan untuk menggabungkan beberapa interface jaringan Hotspot agar berada dalam satu segmen jaringan yang sama. Pada implementasi ini, beberapa interface Hotspot digabungkan ke dalam Bridge1-HOTSPOT.

![Interface List Bridge Hotspot](/images/03-bridge.jpg)

---

# 3.3 Konfigurasi DHCP Client

DHCP Client digunakan agar MikroTik memperoleh alamat IP secara otomatis dari perangkat Starlink sebagai sumber koneksi internet.

Konfigurasi dilakukan melalui menu:

IP → DHCP Client

![Konfigurasi DHCP Client](/images/04-dhcp-client.jpg)

---

# 3.4 Konfigurasi IP Address

IP Address digunakan untuk memberikan alamat jaringan lokal pada interface Bridge1-HOTSPOT sebagai gateway bagi perangkat pengguna.

Konfigurasi dilakukan melalui menu:

IP → Addresses

![Konfigurasi IP Address](/images/05-ip-address.jpg)

---

# 3.5 Konfigurasi DHCP Server untuk Jaringan Hotspot

DHCP Server digunakan untuk memberikan alamat IP secara otomatis kepada perangkat pengguna yang terhubung melalui jaringan Hotspot. Konfigurasi dilakukan pada interface **Bridge1-HOTSPOT** sehingga setiap perangkat yang terhubung ke jaringan dapat memperoleh alamat IP sesuai dengan rentang yang telah ditentukan.

---

### Langkah 1 - Membuka Menu DHCP Setup

Masuk ke menu **IP → DHCP Server**, kemudian pilih **DHCP Setup** untuk memulai proses konfigurasi DHCP Server.

![Langkah 1 - DHCP Setup](/images/06-dhcp-server-bridge11.jpg)

---

### Langkah 2 - Memilih Interface DHCP Server

Pilih interface **Bridge1-HOTSPOT** sebagai interface yang akan digunakan untuk mendistribusikan alamat IP kepada perangkat pengguna.

![Langkah 2 - Interface DHCP Server](/images/dhcp-2.jpg)

---

### Langkah 3 - Menentukan Network Address

Masukkan atau konfirmasikan alamat jaringan (Network Address) yang akan digunakan oleh DHCP Server sesuai dengan konfigurasi jaringan lokal.

![Langkah 3 - Network Address](/images/dhcp-3.jpg)

---

### Langkah 4 - Menentukan Gateway

Tentukan alamat **Gateway** yang akan digunakan oleh seluruh perangkat client sebagai jalur menuju jaringan internet.

![Langkah 4 - Gateway](/images/dhcp-4.jpg)

---

### Langkah 5 - Menentukan Rentang Alamat IP (Address Pool)

Tentukan rentang alamat IP (Address Pool) yang akan dibagikan secara otomatis kepada perangkat yang terhubung ke jaringan Hotspot.

![Langkah 5 - Address Pool](/images/dhcp-5.jpg)

---

### Langkah 6 - Konfigurasi DNS Server

Masukkan alamat DNS Server yang akan digunakan agar perangkat client dapat melakukan resolusi nama domain ke alamat IP.

![Langkah 6 - DNS Server](/images/dhcp-6.jpg)

---

### Langkah 7 - Pengaturan Lease Time

Atur nilai **Lease Time** sebagai lama waktu peminjaman alamat IP sebelum dilakukan pembaruan oleh DHCP Server.

![Langkah 7 - Lease Time](/images/dhcp-7.jpg)

---

### Langkah 8 - Meninjau Konfigurasi DHCP Server

Periksa kembali seluruh parameter konfigurasi yang telah dimasukkan sebelum menyelesaikan proses konfigurasi DHCP Server.

![Langkah 8 - Review Konfigurasi](/images/dhcp-8.jpg)

---

### Langkah 9 - Memberi user name dan passwordnya

![Langkah 9 - Finish DHCP Setup](/images/dhcp-9.jpg)

---

### Langkah 10 - Hotspot sukse

Hotspot telah berhasil aktiv
![Langkah 10 - DHCP Server Aktif](/images/dhcp-10.jpg)
---

# 3.7 Aktivasi DHCP Server untuk Jaringan Hotspot

Setelah seluruh parameter DHCP Server dikonfigurasi, layanan DHCP Server diaktifkan untuk jaringan Hotspot agar perangkat pengguna dapat memperoleh alamat IP secara otomatis.

![Aktivasi DHCP Server Hotspot](../images/08-aktivasi-dhcp-server-hotspot.jpg)

---

# 3.8 Konfigurasi NAT (Network Address Translation)

NAT digunakan untuk menerjemahkan alamat IP jaringan lokal agar perangkat pengguna dapat mengakses internet melalui koneksi Starlink.

Konfigurasi dilakukan melalui menu:

IP → Firewall → NAT

![Konfigurasi NAT](../images/09-nat.jpg)

---

# 3.9 Konfigurasi Hotspot MikroTik

Hotspot digunakan untuk mengatur mekanisme autentikasi pengguna sebelum mendapatkan akses internet. Sistem ini digunakan untuk mendukung layanan akses internet berbasis voucher.

![Konfigurasi Hotspot](../images/10-hotspot.jpg)

---

# 3.10 Konfigurasi User Profile dan User Hotspot

User Profile digunakan untuk mengatur batas waktu dan hak akses pengguna, sedangkan User Hotspot digunakan untuk membuat akun pengguna yang dapat melakukan autentikasi pada jaringan.

![User Profile Hotspot](../images/11-user-profile.jpg)

---

# 4. Pengujian Jaringan

Pengujian dilakukan untuk mengetahui performa jaringan internet Starlink setelah dilakukan konfigurasi MikroTik.

Parameter pengujian meliputi:

- Delay
- Jitter
- Packet Loss
- Throughput

## 4.1 Pengujian Ping

Pengujian ping dilakukan menggunakan alamat DNS Cloudflare (1.1.1.1) dan Google DNS (8.8.8.8).

![Pengujian Ping](../images/12-ping.jpg)

---

## 4.2 Pengujian Throughput

Pengujian throughput dilakukan menggunakan aplikasi Speedtest untuk mengetahui kemampuan bandwidth download dan upload dari layanan Starlink.

![Pengujian Speedtest](../images/13-speedtest.jpg)
