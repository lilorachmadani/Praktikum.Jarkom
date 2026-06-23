# MODUL 14 WIFI

Wi-Fi adalah teknologi jaringan nirkabel yang menggunakan standar **IEEE 802.11** untuk menghubungkan perangkat tanpa kabel. Dengan Wi-Fi, perangkat seperti laptop dan smartphone dapat berkomunikasi serta mengakses internet melalui gelombang radio.

## Perbandingan Frekuensi Wi-Fi

### Frekuensi 2,4 GHz

**Kelebihan:**

* Jangkauan sinyal lebih luas.
* Lebih baik menembus dinding dan penghalang.
* Cocok untuk area yang besar.

**Kekurangan:**

* Kecepatan lebih rendah.
* Lebih mudah mengalami gangguan dari perangkat lain.

### Frekuensi 5 GHz

**Kelebihan:**

* Kecepatan transfer data lebih tinggi.
* Gangguan sinyal lebih sedikit.
* Cocok untuk streaming dan gaming.

**Kekurangan:**

* Jangkauan lebih pendek.
* Sinyal lebih sulit menembus dinding.

## Access Point (AP)

Access Point (AP) adalah perangkat yang memancarkan sinyal Wi-Fi agar perangkat nirkabel dapat terhubung ke jaringan. AP juga membantu memperluas cakupan jaringan sehingga koneksi dapat menjangkau area yang lebih luas.

## Analisis Beacon Frame
<img width="1918" height="1001" alt="image" src="https://github.com/user-attachments/assets/3f5c007e-c9c7-44c9-9501-7bf5a65bbf4b" />

Setelah filter **`wlan.fc.subtype == 8 && wlan.fc.type == 0`** diterapkan, Wireshark menampilkan paket **Beacon Frame** yang dikirim secara berkala oleh access point. Terlihat beberapa SSID seperti **"30 Munroe St"** dan **"linksys12"** dengan nilai **Beacon Interval (BI) = 100**. Dari total **2364 paket** yang tertangkap, terdapat **762 paket Beacon Frame** yang sesuai dengan filter. Paket ini berfungsi untuk mengumumkan keberadaan jaringan Wi-Fi kepada perangkat di sekitarnya.

## Analisis Detail Frame
<img width="1918" height="1022" alt="image" src="https://github.com/user-attachments/assets/5c635a52-75aa-4d7e-a314-5d267b8cc426" />

Pada **Frame 3**, paket yang dipilih merupakan **Beacon Frame** yang dikirim oleh access point dengan MAC Address **00:16:b6:f7:1d:51** ke alamat **broadcast (ff:ff:ff:ff:ff:ff)**. Paket ini berisi informasi dasar jaringan yang dapat dibaca oleh perangkat lain untuk menemukan jaringan Wi-Fi yang tersedia.

## Analisis Tagged Parameters

* **SSID = "30 Munroe St"** menunjukkan nama jaringan Wi-Fi.
* **Supported Rates = 1, 2, 5.5, dan 11 Mbps** menunjukkan kecepatan dasar yang didukung.
* **Current Channel = 6** menandakan access point bekerja pada kanal 6.
* **TIM (Traffic Indication Map)** digunakan untuk memberi informasi adanya data yang menunggu untuk dikirim ke klien.
* **Country Information = US, Indoor** menunjukkan konfigurasi wilayah dan lingkungan penggunaan.
* **Extended Supported Rates** menampilkan kecepatan tambahan hingga **54 Mbps**.
* **Vendor Specific** berisi informasi tambahan dari vendor perangkat dan dukungan fitur Wi-Fi.

Dari hasil analisis dapat disimpulkan bahwa Beacon Frame digunakan oleh access point untuk menyiarkan informasi jaringan secara berkala sehingga perangkat di sekitarnya dapat mendeteksi dan terhubung ke jaringan Wi-Fi tersebut.

## Analisis Data Transfer
<img width="1918" height="1023" alt="image" src="https://github.com/user-attachments/assets/9a3c0b1e-08f3-419c-b96c-9b07df6da983" />

Berdasarkan hasil capture Wireshark dengan filter **`ip.addr == 128.119.245.12`**, terlihat komunikasi antara host **192.168.1.109** dan server **128.119.245.12**. Sebelum data dikirim, terjadi proses pembentukan koneksi TCP melalui tahapan **SYN, SYN-ACK, dan ACK**.Setelah koneksi berhasil dibuat, pada **Frame 480** terlihat paket **HTTP GET /wireshark-labs/alice.txt HTTP/1.1** yang dikirim dari klien ke server. Permintaan tersebut digunakan untuk meminta file **alice.txt** dari server.Server kemudian merespons permintaan tersebut melalui beberapa segmen TCP yang terlihat pada frame berikutnya. Pada detail paket juga terlihat bahwa komunikasi menggunakan **IPv4** dengan **port sumber 2538** dan **port tujuan 80 (HTTP)**.Dari hasil pengamatan dapat disimpulkan bahwa klien berhasil membangun koneksi TCP dengan server dan mengirim permintaan HTTP untuk mengakses file **alice.txt**, kemudian server mengirimkan data yang diminta kepada klien.

## Analisis Proses Association & Disassociation

- **Association (Asosiasi)** merupakan proses saat perangkat klien melakukan koneksi ke Access Point (AP) agar dapat bergabung ke jaringan Wi-Fi. Pada tahap ini, klien mengirimkan permintaan koneksi dan Access Point memberikan respons untuk mengizinkan atau menolak koneksi tersebut. Jika berhasil, perangkat dapat mulai bertukar data melalui jaringan nirkabel.

- **Disassociation (Disasosiasi)** adalah proses pemutusan koneksi antara klien dan Access Point. Proses ini dapat terjadi karena pengguna memutus koneksi secara manual, perangkat berpindah ke Access Point lain, atau karena kondisi jaringan seperti sinyal yang lemah dan gangguan koneksi.

- Pada praktikum ini, proses Association dan Disassociation diamati menggunakan Wireshark dengan menerapkan filter yang sesuai. Dari paket yang ditampilkan, dapat terlihat proses pertukaran pesan antara klien dan Access Point saat membangun maupun mengakhiri koneksi. Hasil pengamatan menunjukkan bahwa proses ini berperan penting dalam pengelolaan koneksi perangkat pada jaringan Wi-Fi sebelum komunikasi data dapat dilakukan.

## Analisis Association Request

### Expand Packet Awal
<img width="1918" height="1022" alt="image" src="https://github.com/user-attachments/assets/de6e5415-5fcb-4bdb-b0e0-10b778cd03ff" />

Pada **Frame 1750**, perangkat **Intel_d1:b6:4f** mengirim paket **Association Request** ke Access Point **CiscoLinksys_f5:ba:bb** dengan SSID **"linksys_SES_24086"**. Paket ini menandakan bahwa klien sedang mengajukan permintaan untuk bergabung ke jaringan Wi-Fi tersebut. Pada bagian parameter paket juga terlihat informasi mengenai kecepatan transmisi yang didukung serta konfigurasi keamanan jaringan berbasis WPA.

### Expand Packet Akhir
<img width="1915" height="1013" alt="image" src="https://github.com/user-attachments/assets/8982eb59-14a1-4e5a-b070-47e30d4571d9" />

Pada **Frame 2162**, klien kembali mengirim **Association Request**, tetapi ke Access Point yang berbeda yaitu **CiscoLinksys_f7:1d:51** dengan SSID **"30 Munroe St"**. Paket ini berisi informasi tambahan seperti **QoS Capability** dan **Extended Supported Rates**, yang menunjukkan fitur dan kecepatan komunikasi yang dapat digunakan pada jaringan tersebut.

### Kesimpulan

Hasil pengamatan menunjukkan bahwa perangkat klien melakukan proses asosiasi ke beberapa Access Point sebelum menentukan jaringan yang akan digunakan. Perbedaan utama kedua paket terletak pada SSID dan Access Point tujuan yang menunjukkan adanya perpindahan atau pemilihan jaringan Wi-Fi oleh klien.

## Analisis Association Response
![Uploading image.png…]()

Untuk melihat tanggapan dari Access Point, digunakan filter **`wlan.fc.type_subtype == 1`**. Hasil capture menampilkan paket **Association Response** yang dikirim oleh **CiscoLinksys_f7:1d:51** kepada perangkat **Intel_d1:b6:4f**.

Paket ini menunjukkan bahwa permintaan asosiasi dari klien telah diterima. Selain itu, Access Point mengirimkan informasi terkait kemampuan jaringan seperti **Supported Rates**, **Extended Supported Rates**, dan **EDCA Parameter Set** yang akan digunakan selama komunikasi berlangsung.

### Kesimpulan

Berdasarkan paket Association Response yang diterima, dapat diketahui bahwa proses asosiasi berhasil dilakukan. Setelah tahap ini selesai, perangkat klien telah terdaftar pada Access Point dan dapat mulai bertukar data melalui jaringan Wi-Fi.
