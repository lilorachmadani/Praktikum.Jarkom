# MODUL 10 IP

Internet Protocol (IP) merupakan alamat identitas yang diberikan kepada setiap perangkat yang terhubung dalam suatu jaringan. Alamat ini memungkinkan perangkat untuk saling mengenali dan bertukar data dengan benar. Dalam proses komunikasi jaringan, IP berperan penting untuk menentukan asal dan tujuan pengiriman informasi sehingga data dapat sampai ke perangkat yang dituju tanpa kesalahan.

## Langkah-Langkah
1. Buka Command Prompt (CMD), kemudian masukkan perintah ipconfig untuk menampilkan informasi konfigurasi jaringan pada perangkat.
<img width="1257" height="695" alt="image" src="https://github.com/user-attachments/assets/ce0dc669-13f6-4a67-b988-9cea1d48d814" />

Hasil konfigurasi menunjukkan bahwa perangkat memperoleh alamat IPv4 192.168.0.112 pada jaringan Wi-Fi yang sedang digunakan. Alamat tersebut termasuk ke dalam rentang alamat private kelas C, yang umumnya digunakan pada jaringan lokal seperti rumah, sekolah, atau kantor.Perangkat juga menggunakan Subnet Mask 255.255.255.0 yang berfungsi untuk menentukan batas antara alamat jaringan dan alamat host. Selain itu, terdapat Default Gateway 192.168.0.1 yang bertugas menghubungkan perangkat ke jaringan lain, termasuk internet. Berdasarkan informasi tersebut, dapat disimpulkan bahwa perangkat telah terhubung dengan jaringan secara normal dan siap digunakan untuk melakukan komunikasi data maupun mengakses berbagai layanan internet.

# TRACEROUTE

Traceroute adalah salah satu tools jaringan yang digunakan untuk melihat jalur yang ditempuh paket data saat dikirim dari komputer pengguna menuju server tujuan. Setiap perangkat jaringan yang dilewati akan ditampilkan secara berurutan beserta waktu responsnya. Informasi ini dapat digunakan untuk mengetahui proses perjalanan data, mengecek kualitas koneksi, serta membantu menemukan titik masalah apabila terjadi gangguan pada jaringan.

## Langkah-Langkah
1. Buka Command Prompt (CMD), kemudian jalankan perintah tracert google.com
<img width="862" height="433" alt="image" src="https://github.com/user-attachments/assets/fcd22da4-fc0e-4ac2-9e87-08d883668514" />
Berdasarkan hasil traceroute, paket data memerlukan 11 hop untuk mencapai server Google dengan alamat 216.239.38.120. Perjalanan dimulai dari 192.168.0.1 yang merupakan gateway utama pada jaringan lokal. Selanjutnya paket diteruskan melalui beberapa router internal milik penyedia layanan internet, yaitu 192.168.1.1, 10.45.0.1, 172.16.33.33, 172.16.35.141, dan 172.17.2.54.
Pada hop ke-7 muncul keterangan "Request timed out", yang menandakan bahwa perangkat pada jalur tersebut tidak memberikan balasan terhadap permintaan traceroute. Kondisi ini tidak selalu menunjukkan adanya gangguan jaringan karena beberapa router memang sengaja tidak merespons paket traceroute.Setelah melewati tahap tersebut, paket melanjutkan perjalanan melalui beberapa router publik dengan alamat 72.14.216.48, 72.14.235.235, dan 142.251.240.255 sebelum akhirnya mencapai server tujuan. Waktu respons yang tercatat berada pada kisaran 1 ms hingga 35 ms, yang menunjukkan bahwa koneksi jaringan cukup stabil dan mampu menjangkau server Google tanpa kendala berarti.

# ICMP, MTU, TTL

**ICMP (Internet Control Message Protocol)** merupakan protokol yang digunakan untuk mengirim informasi terkait kondisi jaringan, seperti laporan kesalahan dan pengecekan koneksi. ICMP sering digunakan pada perintah **ping** dan **traceroute** untuk membantu analisis jaringan.

**MTU (Maximum Transmission Unit)** adalah ukuran maksimum data yang dapat dikirim dalam satu paket melalui jaringan tanpa perlu dipecah menjadi beberapa bagian. Pada jaringan Ethernet, nilai MTU yang umum digunakan adalah **1500 byte**.

**TTL (Time To Live)** adalah nilai yang menentukan batas jumlah hop atau router yang dapat dilewati sebuah paket data. Nilai TTL akan berkurang setiap kali paket melewati router. Jika nilainya mencapai nol, paket akan dibuang untuk mencegah terjadinya perulangan pengiriman data di jaringan.

# FRAGMENTASI

Fragmentasi adalah mekanisme yang terjadi ketika sebuah paket data memiliki ukuran lebih besar daripada kapasitas maksimum yang dapat dilewatkan oleh jaringan. Agar tetap dapat dikirim, paket tersebut akan dibagi menjadi beberapa bagian yang lebih kecil. Setelah sampai di tujuan, bagian-bagian tersebut akan digabungkan kembali menjadi data yang utuh. Proses ini membantu pengiriman data berukuran besar, tetapi dapat menambah beban kerja jaringan dan memperlambat proses komunikasi jika terjadi terlalu sering.

## Langkah-Langkah
1. Jalankan aplikasi Wireshark dan pilih koneksi jaringan yang sedang digunakan.
2. Mulai proses capture dengan menekan tombol Start.
3. Buka Command Prompt (CMD) kemudian jalankan perintah : ping google.com -l 20
   <img width="978" height="250" alt="image" src="https://github.com/user-attachments/assets/7e0b9b0f-8587-4412-868a-4a1ab08646b1" />
4. Setelah paket berhasil ditangkap, gunakan filter berikut pada Wireshark untuk menampilkan paket yang mengalami fragmentasi : ip.flags.mf == 1 || ip.frag_offset > 0
   <img width="1915" height="1017" alt="image" src="https://github.com/user-attachments/assets/a2dadef4-41f2-436d-acfa-a9080bad1dd0" />
5. Amati informasi paket yang muncul dan lakukan analisis terhadap hasil fragmentasi yang terjadi.

## Analisis Hasil

Berdasarkan hasil pengujian, perintah ping google.com -l 2000 mengirim paket ICMP berukuran 2000 byte ke alamat 216.239.38.120. Seluruh paket tidak menerima balasan sehingga muncul pesan Request Timed Out dengan tingkat packet loss 100%.

Hasil capture Wireshark menunjukkan adanya paket "Fragmented IP protocol", yang menandakan bahwa paket ICMP mengalami fragmentasi karena ukurannya melebihi batas MTU jaringan. Paket dikirim dari 192.168.0.112 menuju 216.239.38.120 dengan ukuran 1514 bytes dan nilai TTL 128.

Dari hasil tersebut dapat disimpulkan bahwa paket ping berukuran besar menyebabkan terjadinya fragmentasi pada lapisan IP. Namun, karena tidak ada balasan dari server tujuan, seluruh paket berakhir dengan Request Timed Out.

# IPv6

IPv6 (Internet Protocol Version 6) adalah versi terbaru dari protokol IP yang digunakan untuk memberikan alamat pada perangkat di jaringan. IPv6 dibuat untuk menggantikan IPv4 karena mampu menyediakan jumlah alamat yang jauh lebih banyak dan mendukung komunikasi jaringan yang lebih efisien.

## Langkah-Langkah
1. Buka file ipv6_sample.pcap di Wireshark.
   <img width="772" height="47" alt="image" src="https://github.com/user-attachments/assets/0f52298f-413b-43fc-953b-71ab1c109bcc" />
2. Masukkan filter ipv6 pada kolom pencarian.
3. Perhatikan paket-paket IPv6 yang ditampilkan.
<img width="1918" height="1006" alt="image" src="https://github.com/user-attachments/assets/30eb0f09-30de-4992-8678-c410db87d966" />

Analisis Hasil

Berdasarkan hasil capture, terlihat komunikasi menggunakan IPv6 dari alamat 2001:db8:1::10 menuju 2a00:1450:4009:80b::200e. Paket yang diamati menggunakan protokol TCP dan TLS/SSL pada port 443 (HTTPS). Terdapat beberapa keterangan TCP Retransmission, yang menunjukkan adanya pengiriman ulang paket selama proses komunikasi. Selain itu, muncul informasi Previous segment not captured, yang menandakan ada paket yang tidak berhasil direkam saat capture berlangsung. Dari hasil tersebut dapat disimpulkan bahwa komunikasi data berjalan menggunakan IPv6 dan terhubung ke layanan HTTPS yang aman, meskipun terjadi beberapa retransmisi paket selama proses pengiriman data.
