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
