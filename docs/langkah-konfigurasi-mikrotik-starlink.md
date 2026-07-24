# Langkah langkah aktivasi jaringan Starlink dan Konfigurasi MikroTik

## Deskripsi

Dokumentasi ini berisi langkah-langkah aktivasi jarinagn Starlink untuk mendapatkan koneksi dari satelit LEO Orbit dan konfigurasi MikroTik pada implementasi jaringan internet berbasis Starlink. Konfigurasi dilakukan dengana membuat identity, user baru untuk admin, penamaan interface untuk setiap port pada mikrotik via winbox, seting bridge hotshpot untuk clien, pengalamatan IP Address, setting DHCP Clien, seting DNS Server, seting firewal NAT, seting DHCP Server, konfigurasi hotspot untuk bridge yang sebelumnya sudah di buat.  

## 1. Persiapan Perangkat

Sebelum melakukan implementasi jaringan internet berbasis Starlink, dilakukan persiapan perangkat yang akan digunakan untuk mendukung proses instalasi, konfigurasi, dan pengujian jaringan. Perangkat yang digunakan dalam implementasi ini meliputi perangkat keras (hardware) dan perangkat lunak (software).

### 1.1 Perangkat Keras (Hardware)

Perangkat keras yang digunakan dalam implementasi jaringan terdiri dari:

1. **Antena Starlink Gen 3 (V4)**  
   Digunakan sebagai perangkat utama penerima koneksi internet berbasis satelit Low Earth Orbit (LEO) SpaceX.

2. **Router Starlink**  
   Digunakan sebagai perangkat penghubung antara antena Starlink dengan jaringan lokal serta menyediakan koneksi awal sebelum diteruskan ke router MikroTik.

3. **Router MikroTik**  
   Digunakan sebagai perangkat manajemen jaringan yang berfungsi untuk mengatur distribusi koneksi internet, konfigurasi IP Address, DHCP Server, NAT, Hotspot, serta manajemen pengguna jaringan.

4. **Access Point**  
   Digunakan untuk memperluas jangkauan jaringan dan mendistribusikan koneksi internet kepada pengguna melalui jaringan nirkabel.

5. **Kabel LAN**  
   Digunakan sebagai media penghubung antar perangkat jaringan, seperti koneksi antara Starlink, MikroTik, dan perangkat pendukung lainnya.

6. **Kabel Fiber Optic (FO)**  
   Digunakan sebagai media transmisi untuk mendistribusikan jaringan menuju beberapa titik pengguna dengan jarak yang lebih jauh.

7. **HTB (Hybrid Terminal Box)**  
   Digunakan sebagai perangkat pendukung pada jaringan Fiber Optic untuk menghubungkan dan mendistribusikan koneksi menuju beberapa titik pengguna.

8. **Laptop/PC**  
   Digunakan untuk melakukan konfigurasi router MikroTik menggunakan aplikasi WinBox serta melakukan proses pengujian jaringan.

9. **Smartphone**  
   Digunakan untuk melakukan aktivasi awal, konfigurasi Wi-Fi, dan pemantauan status perangkat Starlink melalui aplikasi Starlink.

---
# Dokumentasi Perangkat Implementasi

## Antena Starlink

Antena Starlink merupakan perangkat utama yang berfungsi menerima koneksi internet dari satelit Low Earth Orbit (LEO) SpaceX. Antena ditempatkan pada lokasi yang memiliki pandangan langit terbuka agar proses komunikasi dengan satelit dapat berjalan dengan optimal.

![Antena Starlink](/images/01-antena-starlink.jpg)

---

## Router Starlink

Router Starlink berfungsi sebagai perangkat penghubung antara antena Starlink dan jaringan lokal. Perangkat ini digunakan pada tahap awal aktivasi dan konfigurasi layanan internet Starlink.

![Router Starlink](/images/02-router-starlink.jpg)

---

## Router MikroTik

Router MikroTik digunakan sebagai perangkat utama dalam pengelolaan jaringan. MikroTik berfungsi untuk mengatur koneksi internet dari Starlink, melakukan konfigurasi jaringan lokal, serta menyediakan layanan Hotspot bagi pengguna.

![Router MikroTik](/images/03-mikrotik.jpg)

---

## Access Point

Access Point digunakan untuk memperluas jangkauan jaringan dan mendistribusikan koneksi internet kepada pengguna melalui jaringan nirkabel.

![Access Point](/images/04-access-point.jpg)

---

## Access Point Outdoor

Access Point Outdoor digunakan sebagai perangkat distribusi jaringan yang berfungsi untuk memancarkan koneksi internet secara nirkabel kepada pengguna di area layanan jaringan. Perangkat ini dipilih karena memiliki kemampuan untuk digunakan pada lingkungan luar ruangan serta mendukung jangkauan jaringan yang lebih luas.

Pada implementasi jaringan ini, Access Point Outdoor terhubung dengan router MikroTik untuk mendistribusikan koneksi internet menuju pengguna melalui jaringan nirkabel.

![Access Point Outdoor](/images/04-access-point-outdoor.jpg)

## Kabel Fiber Optic dan Perangkat Pendukung

Kabel Fiber Optic dan perangkat pendukung digunakan sebagai media distribusi jaringan menuju beberapa titik pengguna. Penggunaan Fiber Optic bertujuan agar koneksi dapat menjangkau lokasi pengguna dengan jarak yang lebih jauh.

![Fiber Optic dan HTB](/images/05-fiber-optic.jpg)
### 1.2 Perangkat Lunak (Software)

Perangkat lunak yang digunakan dalam implementasi jaringan meliputi:

1. **WinBox**  
   Digunakan untuk melakukan konfigurasi dan manajemen router MikroTik.

2. **Aplikasi Starlink Mobile**  
   Digunakan untuk melakukan aktivasi perangkat Starlink, konfigurasi jaringan Wi-Fi, pengecekan status koneksi, serta proses alignment antena.

3. **Speedtest**  
   Digunakan untuk melakukan pengujian kecepatan koneksi internet Starlink.

4. **Command Prompt/Terminal MikroTik**  
   Digunakan untuk melakukan pengujian koneksi jaringan menggunakan perintah ping.

# 2. Topologi Jaringan

Implementasi jaringan menggunakan Starlink sebagai sumber koneksi internet yang terhubung ke router MikroTik. MikroTik berfungsi sebagai perangkat pengelola jaringan yang melakukan konfigurasi alamat IP, distribusi koneksi internet, serta pengaturan layanan Hotspot kepada pengguna melalui Access Point.

![Topologi Jaringan](/images/01-topologi.jpg)

---

# 3. Aktivasi dan Konfigurasi Starlink

Starlink digunakan sebagai sumber koneksi internet utama dalam implementasi jaringan. Sebelum melakukan konfigurasi pada router MikroTik, perangkat Starlink terlebih dahulu dilakukan proses instalasi, aktivasi, dan sinkronisasi dengan satelit Low Earth Orbit (LEO) SpaceX.

Proses aktivasi dilakukan menggunakan aplikasi Starlink untuk memastikan perangkat telah terhubung dengan jaringan satelit, memperoleh status koneksi **Online**, serta mendapatkan posisi antena yang optimal.

---

## 3.1 Pemasangan Fisik Perangkat Starlink

Tahap awal implementasi dilakukan dengan melakukan pemasangan perangkat Starlink secara fisik.

### Langkah 1 - Menempatkan Antena Starlink

Antena Starlink ditempatkan pada area terbuka tanpa adanya penghalang seperti bangunan, pohon, atau objek lain yang dapat mengganggu komunikasi antara antena dengan satelit.

![Antena Starlink](/images/06-antena-starlink.jpg)

---

### Langkah 2 - Menghubungkan Kabel  dan menghidupkan perangkat Starlink

Kabel Starlink dihubungkan dari bagian bawah antena menuju port antena pada router Starlink Gen 3 (V4).
kemudian Router Starlink dihubungkan ke sumber listrik menggunakan adaptor daya bawaan hingga perangkat menyala dan siap dilakukan proses aktivasi.

![Koneksi Kabel Starlink](/images/07-kabel-starlink.jpg)

---


# 3.2 Aktivasi Wi-Fi Starlink Menggunakan Aplikasi

Setelah perangkat Starlink menyala, proses aktivasi dilakukan menggunakan aplikasi Starlink pada smartphone.

### Langkah 1 - Mengunduh Aplikasi Starlink

Aplikasi Starlink diunduh melalui Google Play Store atau App Store sebagai langkah awal sebelum melakukan konfigurasi perangkat.

![Aplikasi Starlink](/images/09-aplikasi-starlink.jpg)

---

### Langkah 2 - Menghubungkan Smartphone ke Wi-Fi Starlink

Buka aplikasi Starlink kemudian pilih menu **Connect to Starlink WiFi** untuk menghubungkan smartphone ke jaringan Wi-Fi bawaan Starlink.
Setelah itu hubungkan smartphone ke jaringan Wi-Fi bawaan STARLINK melalui menu pengaturan Wi-Fi. Dan pada Aplikasi Starlink menampilkan status Online, kemudian  Pilih Starlink Misaligned untuk mengkonfigurasi nama jaringan (SSID) dan kata sandi (password).


![Connect to Starlink WiFi](/images/10-connect-starlink-wifi.jpg)
![Connect to Starlink WiFi](/images/11-connect-starlink-wifi.jpg)
![Connect to Starlink WiFi](/images/12-connect-starlink-wifi.jpg)


---

### Langkah 3 - 3)	Ubah Nama & Kata Sandi Wi-Fi: 

Setelah perangkat Starlink berhasil terhubung ke internet, langkah berikutnya adalah Buka kembali Aplikasi starlink mobilenya untuk melakukan proses mengubah nama jaringan (SSID) dan kata sandi (password) Wi-Fi agar lebih mudah dikenali dan aman digunakan. Proses ini dilakukan melalui aplikasi Starlink dengan mengikuti petunjuk yang tersedia.Kemudian Hubungkan smartphone ke jaringan Wi-Fi bawaan STARLINK,Setelah itu kembali ke aplikasi Starlink. Lalu Masukkan nama jaringan (SSID) dan kata sandi (password) yang diinginkan pada menu Configure WiFi, lalu pilih Submit.Setelah itu Aplikasi menerapkan pengaturan (Applying settings) hingga proses konfigurasi selesai. Setelah selesai, Wi-Fi Starlink akan menggunakan nama dan kata sandi yang baru.

![Status Online Starlink](/images/11-starlink-online.jpg)
![Status Online Starlink](/images/12-starlink-online.jpg)
![Status Online Starlink](/images/13-starlink-online.jpg)


---

# 3.3 Konfigurasi Nama Wi-Fi (SSID) dan Password

Konfigurasi Wi-Fi dilakukan untuk mengubah nama jaringan dan kata sandi bawaan Starlink agar lebih mudah dikenali serta meningkatkan keamanan jaringan.

### Langkah 1 - Membuka Menu Configure WiFi

Masuk kembali ke aplikasi Starlink kemudian pilih menu konfigurasi Wi-Fi.

![Menu Configure WiFi](/images/12-configure-wifi.jpg)

---

### Langkah 2 - Mengatur SSID dan Password

Masukkan nama jaringan (SSID) dan kata sandi (password) yang akan digunakan, kemudian simpan konfigurasi.

![Pengaturan SSID Password](/images/13-ssid-password.jpg)

---

### Langkah 3 - Menerapkan Pengaturan Wi-Fi

Aplikasi Starlink akan menerapkan perubahan konfigurasi hingga proses selesai.

![Applying Settings](/images/14-applying-settings.jpg)

---

# 3.4 Penyelarasan Antena Starlink (Alignment)

Proses alignment dilakukan untuk mendapatkan posisi antena yang optimal dalam menerima sinyal dari satelit Starlink.

### Langkah 1 - Membuka Menu Alignment

Pada halaman utama aplikasi Starlink, pilih menu **Starlink Misaligned** untuk memulai proses penyelarasan antena.

![Starlink Misaligned](/images/15-starlink-misaligned.jpg)

---

### Langkah 2 - Mengikuti Panduan Arah Antena

Aplikasi Starlink akan menampilkan panduan arah berupa indikator panah yang digunakan sebagai acuan dalam mengatur posisi antena.

![Panduan Alignment](/images/16-alignment-guide.jpg)

---

### Langkah 3 - Menyesuaikan Posisi Antena

Sesuaikan posisi antena mengikuti arah yang ditampilkan aplikasi hingga posisi antena berada pada titik optimal.

![Penyesuaian Antena](/images/17-adjust-alignment.jpg)

---

### Langkah 4 - Alignment Berhasil

Apabila proses berhasil, aplikasi akan menampilkan status **Starlink is aligned** yang menunjukkan bahwa antena telah berada pada posisi optimal.

![Starlink Aligned](/images/18-starlink-aligned.jpg)

---

# 3.5 Pengujian Kecepatan Starlink

Setelah proses aktivasi dan konfigurasi selesai, dilakukan pengujian kecepatan koneksi internet menggunakan fitur Speedtest pada aplikasi Starlink.

Berdasarkan hasil pengujian diperoleh:

- **Kecepatan Download : 333 Mbps**
- **Kecepatan Upload : 41,3 Mbps**

Hasil pengujian menunjukkan bahwa perangkat Starlink telah berhasil menyediakan koneksi internet sebelum dilakukan proses konfigurasi lanjutan pada router MikroTik.

![Speedtest Starlink](/images/19-speedtest-starlink.jpg)

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

# 3.5 Aktivasi DHCP Server untuk Jaringan Hotspot

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

# 3.6 Konfigurasi DHCP Server untuk Jaringan Hotspot

Setelah seluruh parameter DHCP Server dikonfigurasi, layanan DHCP Server diaktifkan untuk jaringan Hotspot agar perangkat pengguna dapat memperoleh alamat IP secara otomatis.

![Aktivasi DHCP Server Hotspot](../images/08-aktivasi-dhcp-server-hotspot.jpg)

---

# 3.7 Konfigurasi NAT (Network Address Translation)

NAT digunakan untuk menerjemahkan alamat IP jaringan lokal agar perangkat pengguna dapat mengakses internet melalui koneksi Starlink.

Konfigurasi dilakukan melalui menu:

IP → Firewall → NAT

![Konfigurasi NAT](../images/09-nat.jpg)

---

# 3.8 Konfigurasi Hotspot MikroTik

Hotspot digunakan untuk mengatur mekanisme autentikasi pengguna sebelum mendapatkan akses internet. Sistem ini digunakan untuk mendukung layanan akses internet berbasis voucher.

![Konfigurasi Hotspot](../images/10-hotspot.jpg)

---

# 3.9 Konfigurasi User Profile dan User Hotspot

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
