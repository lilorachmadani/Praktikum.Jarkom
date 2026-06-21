# Laporan Praktikum Jarkom Modul 6
Transmission Control Protocol (TCP) adalah protokol yang berfungsi mengatur proses pertukaran data pada jaringan komputer agar berjalan dengan aman dan terstruktur. Protokol ini memastikan informasi yang dikirim oleh suatu perangkat dapat diterima dengan benar oleh perangkat tujuan. TCP bekerja dengan membangun koneksi terlebih dahulu, memeriksa apakah data telah diterima dengan baik, dan mengirim ulang data apabila terjadi gangguan selama proses transmisi. Karena tingkat keandalannya yang tinggi, TCP banyak digunakan pada layanan yang membutuhkan ketepatan data, seperti website, email, dan transfer file.

## 6.2 Menangkap Tansfer TCP dalam Jumlah Besar dari Komputer Pribadi ke Remote Server
Analisis transfer data TCP dilakukan untuk memahami bagaimana data berpindah dari komputer pengguna menuju server melalui jaringan. Dalam praktikum ini, proses tersebut diamati menggunakan Wireshark yang berfungsi sebagai alat pemantau lalu lintas jaringan.Saat proses transfer berlangsung, Wireshark merekam seluruh paket TCP yang melewati jaringan dan menampilkan berbagai informasi penting, seperti alamat sumber dan tujuan, nomor port, ukuran paket, serta detail komunikasi yang terjadi. Data hasil perekaman tersebut dapat digunakan untuk mengevaluasi kualitas koneksi jaringan, mengetahui efisiensi proses pengiriman data, serta menemukan kemungkinan masalah yang muncul selama komunikasi berlangsung. Selain itu, analisis paket juga membantu dalam mendeteksi aktivitas jaringan yang tidak wajar sehingga dapat menjadi langkah awal dalam menjaga keamanan sistem dan jaringan.

## Langkah-Langkah Praktikum
1. Mengunduh File yang Akan Dikirim

Pertama, akses alamat http://gaia.cs.umass.edu/wireshark-labs/alice.txt melalui browser. Setelah halaman terbuka, simpan file tersebut ke komputer dengan cara klik kanan pada halaman lalu pilih menu Save As.
<img width="1917" height="971" alt="image" src="https://github.com/user-attachments/assets/66de039a-00b6-4bc7-90e7-bd1b88a7c1a8" />

2. Membuka Halaman Upload

Selanjutnya, buka halaman http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html yang akan digunakan sebagai media pengunggahan file.
<img width="1918" height="967" alt="image" src="https://github.com/user-attachments/assets/7e3d8c56-df8b-4920-a0eb-3acd43f9ca14" />

3. Mengunggah File

Pilih file alice.txt yang sebelumnya telah disimpan, kemudian lakukan proses upload melalui halaman yang tersedia. Setelah proses pengunggahan dimulai, tampilan halaman akan berubah seperti yang ditunjukkan pada gambar hasil percobaan.
<img width="1918" height="970" alt="image" src="https://github.com/user-attachments/assets/c2498a01-65c4-40d5-b588-4c816d7d6bb9" />

4. Menghentikan Proses Capture

Setelah file berhasil diunggah, hentikan proses perekaman paket pada Wireshark dengan menekan tombol Stop Capture. Kemudian masukkan kata kunci tcp pada kolom filter untuk menampilkan paket-paket TCP yang telah direkam selama proses berlangsung.
<img width="1235" height="44" alt="image" src="https://github.com/user-attachments/assets/82eaf70f-3e58-4d7f-8889-fdc36f244eb7" />

Paket SYN digunakan sebagai langkah awal dalam pembentukan koneksi TCP antara perangkat client dan server. Paket ini merupakan bagian dari mekanisme three-way handshake yang bertujuan memastikan kedua perangkat siap untuk berkomunikasi. Pada tahap ini belum terjadi pengiriman file, karena proses yang berlangsung hanya berupa negosiasi dan pembentukan koneksi.Setelah koneksi berhasil dibuat, data file mulai dikirimkan melalui sejumlah segmen TCP. Pemecahan data menjadi beberapa segmen dilakukan agar proses transmisi lebih teratur, mudah dikontrol, serta memungkinkan pengiriman ulang apabila terdapat paket yang hilang selama perjalanan.
<img width="1263" height="652" alt="image" src="https://github.com/user-attachments/assets/7d87987d-ca78-430f-ab0f-900c76dc9340" />

Sesudah seluruh data berhasil diterima, server mengirimkan pesan balasan berupa HTTP/1.1 200 OK. Kode status tersebut menunjukkan bahwa permintaan yang dikirim oleh client telah diproses dengan sukses dan file yang diunggah telah diterima tanpa kendala oleh server.

## 6.3 Tampilan Awal pada Captured Trace

## Pertanyaan
1. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien (sumber) untuk mentransfer file ke gaia.cs.umass.edu? Cara paling mudah menjawab pertanyaan ini adalah dengan memilih sebuah pesan HTTP dan meneliti detail paket TCP yang digunakan untuk membawa pesan HTTP tersebut.
2. Apa alamat IP dari gaia.cs.umass.edu? Pada nomor port berapa ia mengirim dan menerima segmen TCP untuk koneksi ini?
3. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien Anda (sumber) untuk mentransfer ke gaia.cs.umass.edu?

## Jawaban

1. Berdasarkan hasil pengamatan pada Wireshark, perangkat klien yang digunakan dalam proses pengiriman file memiliki alamat IP **10.225.197.205**. Pada saat komunikasi berlangsung, koneksi TCP menggunakan nomor port sumber **56333** untuk berinteraksi dengan server tujuan.
<img width="1267" height="672" alt="image" src="https://github.com/user-attachments/assets/b3b083b6-ffab-4f8e-91df-4b77b7381c2a" />

2. Server **gaia.cs.umass.edu** teridentifikasi memiliki alamat IP **128.119.245.12**. Selama proses transfer file, server memanfaatkan **port 80** yang merupakan port standar untuk layanan HTTP dalam menerima maupun mengirimkan segmen TCP.
<img width="1265" height="640" alt="image" src="https://github.com/user-attachments/assets/8eea2d55-4b64-428e-a05b-be6db1789c24" />

3. Dari paket yang berhasil ditangkap, diketahui bahwa komputer klien menggunakan alamat IP **10.225.197.205** dengan nomor port **56333** sebagai identitas koneksi TCP. Kombinasi alamat IP dan port tersebut digunakan untuk melakukan komunikasi serta mengirimkan data ke server **gaia.cs.umass.edu**.

## 6.4 Dasar TCP

## Pertanyaan

1. Berapa nomor urut segmen TCP SYN yang digunakan untuk memulai sambungan TCP antara komputer klien dan gaia.cs.umass.edu? Apa yang dimiliki segmen tersebut sehingga teridentifikasi sebagai segmen SYN? 
2. Berapa nomor urut segmen SYNACK yang dikirim oleh gaia.cs.umass.edu ke komputer klien sebagai balasan dari SYN? Berapa nilai dari field Acknowledgement pada segmen SYNACK? Bagaimana gaia.cs.umass.edu menentukan nilai tersebut? Apa yang dimiliki oleh segmen sehingga teridentifikasi sebagai segmen SYNACK? 
3. Berapa nomor urut segmen TCP yang berisi perintah HTTP POST? Perhatikan bahwa untuk menemukan perintah POST, Anda harus menelusuri content field milik paket di bagian bawah jendela Wireshark, kemudian cari segmen yang berisi "POST" di bagian field DATAnya. 
4. Anggap segmen TCP yang berisi HTTP POST sebagai segmen pertama dalam koneksi TCP. Berapa nomor urut dari enam segmen pertama dalam TCP (termasuk segmen yang berisi HTTP POST)? Pada jam berapa setiap segmen dikirim? Kapan ACK untuk setiap segmen diterima? Dengan adanya perbedaan antara kapan setiap segmen TCP dikirim dan kapan acknowledgement-nya diterima, berapakah nilai RTT untuk keenam segmen tersebut? Berapa nilai EstimatedRTT setelah penerimaan setiap ACK? (Catatan: Wireshark memiliki fitur yang memungkinkan Anda untuk memplot RTT untuk setiap segmen TCP yang dikirim. Pilih segmen TCP yang dikirim dari klien ke server gaia.cs.umass.edu pada jendela "daftaraket yang ditangkap". Kemudian pilih: Statistics->TCP Stream Graph- >Round Trip Time Graph). 
5. Berapa panjang setiap enam segmen TCP pertama? 
6. Berapa jumlah minimum ruang buffer tersedia yang disarankan kepada penerima dan diterima untuk seluruh trace? Apakah kurangnya ruang buffer penerima pernah menghambat pengiriman? 
7. Apakah ada segmen yang ditransmisikan ulang dalam file trace? Apa yang anda periksa (di dalam file trace) untuk menjawab pertanyaan ini? 
8. Berapa banyak data yang biasanya diakui oleh penerima dalam ACK? Dapatkah anda mengidentifikasi kasus-kasus di mana penerima melakukan ACK untuk setiap segmen yang diterima? 
9. Berapa throughput (byte yang ditransfer per satuan waktu) untuk sambungan TCP? Jelaskan bagaimana Anda menghitung nilai ini.

## Jawaban
1. Dari hasil analisis paket pada Wireshark, segmen pertama yang digunakan untuk memulai koneksi TCP memiliki **Sequence Number (Seq) = 0**. Segmen tersebut dapat dikenali sebagai paket SYN karena pada kolom informasi terdapat keterangan **[SYN]**, yang menandakan bahwa flag SYN aktif dan digunakan sebagai langkah awal pembentukan koneksi antara client dan server.

2. Pada paket balasan dari server yang bertipe **SYN-ACK**, terlihat bahwa **Sequence Number bernilai 0** dan **Acknowledgement Number bernilai 1**. Nilai ACK tersebut menunjukkan bahwa server telah menerima segmen SYN dari client dan mengakui nomor urut berikutnya yang diharapkan. Paket ini dapat diidentifikasi melalui flag **[SYN, ACK]** yang aktif secara bersamaan sebagai bagian dari proses three-way handshake.

3. Segmen TCP yang membawa permintaan **HTTP POST** memiliki **Sequence Number sebesar 1**. Paket ini ditemukan pada frame ke-4 dan dapat dikenali dari adanya perintah **"POST /ethereal-labs/lab3-1-reply.htm HTTP/1.1"** pada bagian payload. Selain itu, keberadaan flag **[PSH, ACK]** dan ukuran data sebesar **565 byte** menunjukkan bahwa paket tersebut berisi data aplikasi yang dikirim menuju server.

4. Berdasarkan grafik **Round Trip Time (RTT)** yang ditampilkan Wireshark, enam segmen pertama menunjukkan nilai RTT yang berubah-ubah pada rentang sekitar **30 ms hingga 180 ms**. Nilai RTT diperoleh dari titik-titik awal pada grafik pengamatan. Variasi tersebut menunjukkan bahwa waktu tempuh paket di jaringan tidak selalu konstan karena dipengaruhi oleh kondisi lalu lintas jaringan. Sementara itu, nilai **Estimated RTT** dihitung menggunakan metode **Exponential Weighted Moving Average (EWMA)** dengan parameter α = 0,125 sehingga menghasilkan nilai yang lebih stabil dibandingkan RTT aktual.

5. Jika dijumlahkan, ukuran data dari enam segmen TCP pertama mencapai **7.865 byte**. Nilai tersebut diperoleh dari akumulasi panjang data yang dikirim pada keenam segmen awal selama proses transfer berlangsung.

6. Hasil pengamatan menunjukkan bahwa sisi penerima masih memiliki **ruang buffer sebesar 17.520 byte**. Kapasitas ini cukup untuk menampung data yang masuk tanpa menyebabkan hambatan pada proses komunikasi. Tidak ditemukan nilai **Window Size = 0**, sehingga dapat disimpulkan bahwa buffer penerima tidak pernah berada dalam kondisi penuh selama pengiriman data berlangsung.

7. Selama proses transfer berlangsung, tidak ditemukan adanya paket TCP yang mengalami **retransmission**. Kondisi ini mengindikasikan bahwa seluruh paket berhasil diterima dengan baik oleh penerima tanpa kehilangan data yang mengharuskan pengiriman ulang.

8. Jumlah byte yang diakui oleh paket **ACK** tidak selalu memiliki nilai yang sama. Dalam mekanisme TCP, satu ACK dapat mengonfirmasi penerimaan beberapa segmen sekaligus, sehingga jumlah data yang diakui bergantung pada kondisi penerimaan paket dan strategi pengiriman yang digunakan.

9. Dari grafik throughput yang diamati, kecepatan transfer TCP cenderung stabil pada kisaran **200–250 kbps**. Jika dikonversi ke satuan byte, nilainya berada di sekitar **25–31 KB/s**. Nilai tersebut diperoleh dengan memperhatikan garis rata-rata throughput pada grafik dan kemudian mengubah satuan kilobit per detik menjadi kilobyte per detik melalui proses konversi.

## 6.5 Congestion Control pada TCP

**Congestion Control** merupakan mekanisme pada TCP yang berfungsi untuk mengatur jumlah data yang dikirim ke jaringan agar tidak menimbulkan kemacetan. Tujuan utama mekanisme ini adalah menjaga kestabilan jaringan, mengurangi risiko terjadinya kehilangan paket, serta memastikan setiap pengguna memperoleh kesempatan yang adil dalam memanfaatkan bandwidth yang tersedia. Untuk mengendalikan laju pengiriman data, TCP menggunakan parameter **Congestion Window (CWND)** yang nilainya akan berubah sesuai kondisi jaringan. Jika terdeteksi adanya indikasi kemacetan, seperti packet loss atau timeout, TCP akan menyesuaikan ukuran jendela pengiriman sehingga beban jaringan dapat dikurangi.

## Langkah-Langkah dan Analisis

### 1. Mengidentifikasi Fase Slow Start dan Congestion Avoidance

**Langkah Kerja:**

1. Buka file **tcp-ethereal-trace-1** menggunakan Wireshark.
2. Masukkan filter **tcp** pada kolom pencarian agar hanya paket TCP yang ditampilkan.
3. Pilih menu **Statistics → TCP Stream Graph → Time-Sequence Graph (Stevens)**.
4. Amati pola grafik yang dihasilkan.

**Hasil Analisis:**

Berdasarkan grafik Time-Sequence yang diperoleh, fase **slow start** terlihat pada awal proses komunikasi, yaitu sejak pengiriman data dimulai hingga sekitar 0,5 detik pertama. Pada periode ini, pertambahan sequence number meningkat dengan cepat yang menunjukkan bahwa ukuran congestion window terus bertambah.

Setelah melewati fase tersebut, pola pertumbuhan sequence number berubah menjadi lebih teratur dan mendekati garis lurus. Kondisi ini menandakan bahwa TCP telah memasuki fase **congestion avoidance**, yaitu tahap di mana peningkatan laju pengiriman dilakukan secara lebih hati-hati untuk menghindari kemacetan jaringan.

Jika dibandingkan dengan model TCP yang ideal, grafik hasil pengamatan tidak menunjukkan pola eksponensial yang sempurna pada fase slow start. Bentuk grafik yang menyerupai tangga (*staircase pattern*) mengindikasikan adanya pengaruh kondisi jaringan nyata, seperti variasi waktu tempuh paket (RTT), keterlambatan ACK, serta faktor-faktor lain yang memengaruhi proses transmisi data.

### 2. Mengidentifikasi Fase Slow Start dan Congestion Avoidance pada Transfer File alice.txt

**Langkah Kerja:**

1. Jalankan Wireshark dan mulai proses capture pada antarmuka Wi-Fi yang digunakan.
2. Buka halaman **http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html** melalui browser.
3. Unggah file **alice.txt** ke halaman tersebut.
4. Setelah proses upload selesai, kembali ke Wireshark dan gunakan filter **tcp**.
5. Pilih menu **Statistics → TCP Stream Graph → Time-Sequence Graph (Stevens)** untuk melihat pola pengiriman data.

**Hasil Analisis:**

Pada percobaan ini, fase **slow start** tidak terlihat secara jelas seperti yang dijelaskan dalam teori TCP. Sejak awal pengamatan, kenaikan sequence number cenderung berlangsung secara bertahap tanpa menunjukkan peningkatan yang sangat cepat. Grafik yang muncul lebih banyak memperlihatkan pola bertingkat dengan jarak waktu antar pengiriman yang relatif besar.

Dari hasil tersebut dapat disimpulkan bahwa koneksi TCP lebih sering berada pada kondisi **congestion avoidance** atau dipengaruhi oleh faktor eksternal yang membatasi laju pengiriman data. Beberapa faktor yang dapat menyebabkan kondisi tersebut antara lain keterbatasan aplikasi dalam mengirim data, tingginya latency jaringan, karakteristik koneksi Wi-Fi, serta mekanisme flow control yang diterapkan selama komunikasi berlangsung.

Apabila dibandingkan dengan karakteristik TCP ideal, hasil pengamatan menunjukkan adanya perbedaan yang cukup signifikan karena tidak terlihat fase pertumbuhan yang sangat cepat pada awal transmisi. Selain itu, jeda yang muncul antar segmen data menunjukkan bahwa performa jaringan dan aplikasi turut memengaruhi pola pengiriman data yang diamati.
