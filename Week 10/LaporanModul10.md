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
