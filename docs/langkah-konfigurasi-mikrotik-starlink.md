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
--
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

   --

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

### Langkah 3 - Ubah Nama & Kata Sandi Wi-Fi: 

Setelah perangkat Starlink berhasil terhubung ke internet, langkah berikutnya adalah Buka kembali Aplikasi starlink mobilenya untuk melakukan proses mengubah nama jaringan (SSID) dan kata sandi (password) Wi-Fi agar lebih mudah dikenali dan aman digunakan. Proses ini dilakukan melalui aplikasi Starlink dengan mengikuti petunjuk yang tersedia.Kemudian Hubungkan smartphone ke jaringan Wi-Fi bawaan STARLINK,Setelah itu kembali ke aplikasi Starlink. Lalu Masukkan nama jaringan (SSID) dan kata sandi (password) yang diinginkan pada menu Configure WiFi, lalu pilih Submit.Setelah itu Aplikasi menerapkan pengaturan (Applying settings) hingga proses konfigurasi selesai. Setelah selesai, Wi-Fi Starlink akan menggunakan nama dan kata sandi yang baru.

![Status Online Starlink](/images/11-starlink-online.jpg)
![Status Online Starlink](/images/12-starlink-online.jpg)
![Status Online Starlink](/images/13-starlink-online.jpg)


---

## Langkah 4 - Atur Penyelarasan (Alignment): 

Pada tahap ini dilakukan penyelarasan (alignment) antena Starlink agar memperoleh arah yang optimal dalam menerima sinyal satelit. Proses penyelarasan dilakukan melalui aplikasi Starlink dengan mengikuti panduan visual yang ditampilkan pada layar.
Pada halaman utama aplikasi Starlink, pilih menu Starlink misaligned untuk memulai proses penyelarasan antena. Setelah menu dipilih, aplikasi akan menampilkan panduan penyelarasan berupa arah panah dan kotak indikator. Panduan ini digunakan sebagai acuan untuk mengatur posisi antena Starlink. Kemudian Putar atau sesuaikan posisi fisik antena Starlink mengikuti arah panah yang ditampilkan pada aplikasi. Lakukan penyesuaian hingga posisi antena sejajar dengan kotak indikator pada layar. Jika penyelarasan sudah tepat, kotak putih akan menyala terang sebagai tanda bahwa posisi antena telah sesuai. Setelah penyelarasan berhasil, aplikasi akan menampilkan status Starlink is aligned. Pilih tombol “Done” untuk menyelesaikan proses penyelarasan. Dengan demikian, antena Starlink telah berada pada posisi optimal dan siap digunakan.

![Menu Configure WiFi](/images/12-configure-wifi.jpg)

![Menu Configure WiFi](/images/13-configure-wifi.jpg)


![Menu Configure WiFi](/images/14-configure-wifi.jpg)

![Menu Configure WiFi](/images/15-configure-wifi.jpg)
--


# 3.3 Pengujian Kecepatan Starlink

Setelah proses aktivasi dan konfigurasi selesai, dilakukan pengujian kecepatan koneksi internet menggunakan fitur Speedtest pada aplikasi Starlink.

Berdasarkan hasil pengujian diperoleh:

- **Kecepatan Download : 333 Mbps**
- **Kecepatan Upload : 41,3 Mbps**

Hasil pengujian menunjukkan bahwa perangkat Starlink telah berhasil menyediakan koneksi internet sebelum dilakukan proses konfigurasi lanjutan pada router MikroTik.

![Speedtest Starlink](/images/19-speedtest-starlink.jpg)
![Speedtest Starlink](/images/20-speedtest-starlink.jpg)

---

# 4 Konfigurasi perangkat MikroTik RB750Gr3

Setelah jalur utama internet dari Starlink dipastikan aktif dan stabil, dilakukan instalasi logis pada router pusat menggunakan bantuan aplikasi WinBox. Adapun ringkasan alokasi port interface, pengalamatan IP Address, serta DNS Server secara menyeluruh dapat dilihat pada tabel berikut:

## 4.1 Perencanaan Interface dan Alamat IP

Sebelum melakukan proses konfigurasi pada router MikroTik, dilakukan perencanaan interface dan pembagian alamat IP untuk menentukan fungsi masing-masing port jaringan. Perencanaan ini bertujuan agar proses konfigurasi dan distribusi jaringan dapat berjalan sesuai dengan topologi yang telah dirancang.

| No | Interface | Fungsi / Segment Jaringan | Alamat IP Host | Alamat Network |
|----|-----------|---------------------------|----------------|----------------|
| 1 | Ether1-ISP | WAN (Jalur utama koneksi internet dari Starlink) | 192.168.1.163/24 | 192.168.1.0/24 |
| 2 | Bridge1-HOTSPOT<br>(Ether3, Ether4, Ether5) | LAN/WLAN (Segmen jaringan pengguna Hotspot Voucher) | 20.20.20.20/24 | 20.20.20.0/24 |
| 3 | DNS Server Utama | Resolusi domain menggunakan Google Public DNS | 8.8.8.8 | Static DNS Configuration |
| 4 | DNS Server Cadangan | Resolusi domain alternatif menggunakan Google Public DNS | 8.8.4.4 | Static DNS Configuration |

---

## 4.2 Pengaturan Identitas (Identity) dan Proteksi Keamanan Router

Identitas router diubah menjadi Dusun Kotania Atas melalui menu System Identity untuk mempermudah identifikasi remote. Keamanan perangkat kemudian diperketat dengan memberikan password baru pada akun admin di menu System Users untuk mencegah akses ilegal.
1.Halaman Login Via  WinBox
![halaman login winbox](/images/login-winbox.jpg)
 --
2.Tampilan Menu Via  WinBox 
![halaman login winbox](/images/menu-winbox.jpg)
--
3.System Users Pengamanan Kata Sandi Sistem Utama MikroTik Via  WinBox
![halaman login winbox](/images/pengamanan-winbox.jpg)
--

## 4.3 Penamaan Port Interface

Melalui menu Interfaces, port fisik router dinamai ulang secara spesifik: 
•	ether1 menjadi Ether1-ISP, 
•	ether2 menjadi Ether2-PC, 
•	Ether3, Ether4, dan Ether5 menjadi Hotspot1, Hotspot2, dan Hotspot3. 

Penamaan ini bertujuan untuk mempermudah pembagian jalur data, dan ketiganya digabungkan menjadi satu segmen jaringan yang sama melalui sistem Bridge (Bridge Hotspot).

 ![halaman login winbox](/images/4.3-winbox.jpg)
 --
 
 ## 4.4 Integrasi Penggabungan Port (Virtual Bridging)
Untuk menyatukan kontrol voucher, dibuat interface virtual bernama bridge-hotspot. Melalui menu Ports, Ether3-Hotspot1, Ether4-Hotspot2, dan Ether5-Hotspot3 digabungkan ke dalam bridge tersebut sehingga berada dalam satu segmen atau kelas yang sama.

![halaman login winbox](/images/BRIDGE.jpg)

Sebagai bukti dokumentasi nyata pada ini konfigurasi Bridge Hotspot dengan tiga port (Ether3-Hotspot1, Ether4-Hotspot2, dan Ether5-Hotspot3) telah berhasil diterapkan dan aktif mendistribusikan trafik data, berikut disajikan tangkapan layar (screenshot) Interface List dari perangkat MikroTik yang digunakan di lapangan:

--

## 4.5 Aktivasi DHCP Client WAN Via WinBox

Fitur DHCP Client diaktifkan pada port Ether1-ISP. Router otomatis menerima alokasi IP dinamis 192.168.1.163/24 beserta gateway dari modem Starlink hingga statusnya berubah menjadi Bound (terhubung internet

 ![halaman login winbox](/images/DHCP-CLIENT.jpg)
 --
 
 ## 4.6 IP Address List Via WinmBox
 lalui menu IP Address, dialokasikan IP statis untuk jaringan internal, sedangkan interface virtual bridge-hotspot diberikan IP Kelas A yaitu 20.20.20.20/24 yang bertindak sebagai gateway captive portal user.

![halaman login winbox](/images/IP.jpg)
 --
  ## 4.7 Penerapan DHCP Server untuk Titik Distribusi Client Via WinBox
  
  Konfigurasi DHCP Server dilakukan untuk memberikan alamat IP secara otomatis kepada gawai pengguna yang terhubung ke jaringan Hotspot.    Proses ini dimulai dengan menjalankan DHCP Setup Wizard pada menu, seperti ditunjukkan pada 
### Langkah 1 – Membuka Menu DHCP Setup

Buka menu **IP → DHCP Server → DHCP Setup** pada aplikasi WinBox untuk memulai proses konfigurasi DHCP Server.

![halaman login winbox](/images/SETUP1.jpg)

---

### Langkah 2 – Memilih Interface DHCP Server

Pilih interface **Bridge1-HOTSPOT** sebagai interface yang akan digunakan untuk mendistribusikan alamat IP kepada pengguna.

![halaman login winbox](/images/SETUP2.jpg)

---

### Langkah 3 – Mengatur Lease Time

Atur nilai **Lease Time** sesuai kebutuhan, kemudian lanjutkan proses konfigurasi hingga selesai.

![halaman login winbox](/images/SETUP3.jpg)
   
   Pada tahap ini seperti ditunjukkan pada menu DHCP Setup, dilakukan pemilihan DHCP Server Interface yaitu Bridge1-HOTSPOT. Setelah pemilihan antarmuka dilakukan, langkah selanjutnya adalah menekan tombol Next untuk mengonfirmasi parameter teknis seperti DHCP Address Space, Gateway, Address to Give Out, DNS Servers, dan Lease Time. Seluruh parameter tersebut dibiarkan menggunakan nilai default yang telah dihitung otomatis oleh sistem MikroTik sesuai dengan segmen IP yang telah ditentukan sebelumnya.
Proses diakhiri dengan tampilan notifikasi sukses setelah Lease Time. Menandakan bahwa DHCP Server telah aktif dan siap mendistribusikan alamat IP secara dinamis kepada setiap perangkat yang melakukan autentikasi pada jaringan Hotspot Dusun Kotania Atas.

---

## 4.8 Aktivasi DHCP Server untuk Jaringan Hotspot

   Setelah antarmuka bridge-hotspot berhasil dibuat, langkah krusial berikutnya adalah mengaktifkan layanan DHCP Server agar setiap gawai warga yang terhubung ke jaringan Wi-Fi mendapatkan konfigurasi IP Address secara otomatis (dinamis). Aktivasi ini dilakukan melalui DHCP Setup Wizard pada menu ip dhcp-server. Proses konfigurasi ini melibatkan penenuan interface Bridge-Hotspot sebagai pintu gerbang utama yang akan memfilter trafik pengguna. Dengan mengaktifkan fitur ini, sistem akan secara otomatis melakukan redirect (pengalihan) pada setiap permintaan HTTP dari perangkat klien menuju halaman login yang telah dirancang.
  
   gambar gambar berikut adalah Alur Konfigurasi DHCP Server untuk Bridge1-HOTSPOT

 ![halaman login winbox](/images/brid-1.jpg)
 --
 ![halaman login winbox](/images/brid-2.jpg)
 --
 ![halaman login winbox](/images/48-3.jpg)
  --
 ![halaman login winbox](/images/48-4.jpg)
   --
![halaman login winbox](/images/lima.jpg)
   --
![halaman login winbox](/images/enam.jpg)
--
![halaman login winbox](/images/tuju.jpg)
 --
![halaman login winbox](/images/delapan.jpg)
--
![halaman login winbox](/images/sembilan.jpg)
--
![halaman login winbox](/images/sepuluh.jpg)
--

Seluruh parameter teknis pada gambar diatas diselesaikan dengan memilih opsi Next secara berurutan hingga sistem memberikan notifikasi "Setup has completed successfull

---

## 4.9 Translasi Alamat Jaringan via Firewall NAT

Agar seluruh segmen IP privat lokal dapat mengakses internet, dibuat aturan baru pada menu IP Firewall NAT. Parameter disetel menggunakan Chain: srcnat, Out. Interface: Ether1-ISP, dan Action: masquerade. Aturan ini berfungsi menyamarkan IP lokal menjadi IP publik Starlink yang valid di internet.

![halaman login winbox](/images/nat.jpg)
--
![halaman login winbox](/images/natt.jpg)
--
NAT Masquerade berfungsi menerjemahkan alamat IP private pada jaringan lokal menjadi alamat IP publik Starlink sehingga seluruh perangkat pengguna dapat mengakses internet.

---
# 5.Configurasi perangkat access point(AP) untuk client (user)

Gambar-gambar berikut menjelaskan langkah-langkah konfigurasi perangkat router menjadi access point(AP) untuk client(user).Berikut langkah-langkahnya:

### 1. memasukan IP default router di browser

   ![halaman login winbox](/images/acess1.jpg)
   ---
   
### 2. masukan password kemudian login ke sistem setingannya

   ![halaman login winbox](/images/acess2.jpg)
   ---

### 3. pilih menu quick setup lalu pilih next

  ![halaman login winbox](/images/acess3.jpg)
  ---

### 4. pilih access point lalu next

![halaman login winbox](/images/acess4.jpg)
 ---

## 5. ganti nama access point kemudian pilih disable wireless security, lalu next

![halaman login winbox](/images/acess5.jpg)
  ---

## 6. pilih next

![halaman login winbox](/images/acess6.png)
  ---

## 7. pilih finish

![halaman login winbox](/images/acess7.png)
---

## 8. tunggu sampai proses rebootingnya selesai

![halaman login winbox](/images/acess8.png)
---

## 9. jika sudah maka masukkan password yang sudah di buat sebelumnya pada tampilan login

![halaman login winbox](/images/acess9.png)
---

## 10. pilih sistem tools untuk mengatur zona waktunya

![halaman login winbox](/images/acess10.png)
---
