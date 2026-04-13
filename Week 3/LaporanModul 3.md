# Laporan Praktikum Jarkom Modul 3

# Basic HTTP GET
Proses ini bertujuan untuk mengamati mekanisme komunikasi antara client (browser) dan server yang berlangsung melalui metode HTTP GET serta respons HTTP (HTTP Response).
## Langkah-Langkah
1.Buka aplikasi wireshark
![Lampiran](../assets/image/HTTP%20GET%20(1).png)
2.Jika sudah membuka aplikasi wireshark lalu pilih menu wifi
![Lampiran](../assets/image/HTTP%20GET%20(2).png)
3.Selanjutnya buka chrome dan jalankan browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html 
![Lampiran](../assets/image/HTTP%20GET%20(3).png)
4.Setelah itu kembali ke aplikasi wireshark dan gunakan fitur filter dan ketik http
![Lampiran](../assets/image/gambar%20wireshark%20(4).png)
5.Stop capture dan pada paket yang di pilih akan muncul rincian paket
![Lampiran](../assets/image/HTTP%20GET%20(4).png)

# WEB Not Found
Pada percobaan ini, dilakukan pengujian sederhana untuk mengetahui bagaimana proses pencarian ketika menggunakan alamat web yang bersifat acak, namun tetap memanfaatkan protokol HTTP sebagai media aksesnya.
## Langkah-Langkah
1.Buka aplikasi wireshark, lalu pilih menu wifi
![Lampiran](../assets/image/HTTP%20GET%20(2).png)
2.Selanjutnya buka chrome dan jalankan browser asal http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.htmlregergev
![Lampiran](../assets/image/Not%20Found%202.png)
3.Setelah itu kembali ke aplikasi wireshark dan gunakan fitur filter dan ketik http
![Lampiran](../assets/image/gambar%20wireshark%20(4).png)
4.Stop capture dan pada paket yang di pilih akan muncul keterangan 404 atau eror
![Lampiran](../assets/image/Not%20Found.png)

# Retrieving Long Documents
pembahasan difokuskan pada proses Retrieving Long Document, yaitu proses pengambilan data berukuran besar seperti file, halaman web, atau dokumen panjang. Data tersebut diperoleh dari hasil penangkapan (capture) paket jaringan yang ditransmisikan melalui berbagai protokol komunikasi, seperti HTTP, TCP, maupun FTP.
## Langkah-Langkah
1.Buka aplikasi wireshark, lalu pilih menu wifi
![Lampiran](../assets/image/HTTP%20GET%20(2).png)
2.Selanjutnya buka chrome dan jalankan browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
![Lampiran](../assets/image/Retrieving%20Long%20Documents%20(1).png)
3.Setelah itu kembali ke aplikasi wireshark dan gunakan fitur filter dan ketik http
![Lampiran](../assets/image/gambar%20wireshark%20(4).png)
4.Stop capture dan pada paket yang di pilih akan muncul rincian paket
![Lampiran](../assets/image/Retrieving%20Long%20Documents%20(3).png)

# HTML Documents Dengan Embedded Objects
Pembahasan mengenai HTML Documents with Embedded Objects, yaitu dokumen HTML yang memuat objek tambahan seperti gambar, CSS, JavaScript, maupun file lainnya. Keberadaan objek-objek tersebut menyebabkan browser mengirimkan beberapa permintaan (request) HTTP saat halaman dibuka, yang selanjutnya dapat diamati melalui proses capture menggunakan Wireshark.
## Langkah-Langkah
1.Buka aplikasi wireshark, lalu pilih menu wifi
![Lampiran](../assets/image/HTTP%20GET%20(2).png)
2.Selanjutnya buka chrome dan jalankan browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html
![Lampiran](../assets/image/Embedded%20Objects%20(1).png)
3.Setelah itu kembali ke aplikasi wireshark dan gunakan fitur filter dan ketik http
![Lampiran](../assets/image/gambar%20wireshark%20(4).png)
4.Stop capture dan pada paket yang di pilih akan muncul rincian terlihat tulisan jpeg dikarenakan pada link tersebut saat di search terdapat gambar jadi pada wireshark menampilkan data atau mendeteksi pada web tersebut terdapat gambar
![Lampiran](../assets/image/Embedded%20Objects%20(2).png)

# HTTP Authentication
Pembahasan mengenai HTTP Authentication, yaitu proses autentikasi (login) yang terjadi ketika klien mengakses sebuah website yang memerlukan username dan password. Proses ini melibatkan pertukaran data melalui protokol HTTP, yang dapat diamati pada paket jaringan hasil capture menggunakan Wireshark.
## Langkah-Langkah
1.Buka aplikasi wireshark, lalu pilih menu wifi
![Lampiran](../assets/image/HTTP%20GET%20(2).png)
2.Selanjutnya buka chrome dan jalankan browser http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html
![Lampiran](../assets/image/HTTP%20Authentication%20(1).png)

3.Masukkan username:wireshark-students dan password:network lalu tekan enter

![Lampiran](../assets/image/HTTP%20Authentication%20(2).png)

4.Jika sudah browser akan menampilkan seperti ini
![Lampiran](../assets/image/HTTP%20Authentication%20(3).png)
5.Setelah itu kembali ke aplikasi wireshark dan gunakan fitur filter dan ketik http
![Lampiran](../assets/image/gambar%20wireshark%20(4).png)
6.Stop capture dan pada paket yang di pilih akan muncul rincian Unauthorized
![Lampiran](../assets/image/HTTP%20Authentication%20(4).png)
