# Laporan Praktikum Jarkom Modul 5
UDP (User Datagram Protocol) adalah protokol komunikasi yang digunakan untuk mengirim data secara cepat tanpa mekanisme pengecekan atau konfirmasi. Berbeda dengan TCP, UDP tidak menjamin keandalan, sehingga tidak ada pengurutan maupun perbaikan data yang hilang.

## Langkah-Langkah
1.Download file dari link berikut http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
2.extrack file yang sudah di download dari link tersebut
![Lampiran](../assets/image/Modul%205.png)
3.Setelah di extract pilih file bernama "http-ethereal-trace-5" dan buka menggunakan wireshark
![Lampiran](../assets/image/Modul%205%20(2).png)
4.Setelah membuka file nya menggunakan wireshark ketik udp pada kolom filter agar terfilter
![Lampiran](../assets/image/Modul%205%20(3).png)

## Pertanyaan
1. Pilih satu paket UDP yang terdapat pada trace Anda. Dari paket tersebut, berapa banyak “field” yang terdapat pada header UDP? Sebutkan nama-nama field yang Anda temukan!
2. Perhatikan informasi “content field” pada paket yang Anda pilih di pertanyaan 1. Berapa panjang (dalam satuan byte) masing-masing “field” yang terdapat pada header UDP?
3. Nilai yang tertera pada ”Length” menyatakan nilai apa? Verfikasi jawaban Anda melalui paket UDP pada trace.
4. Berapa jumlah maksimum byte yang dapat disertakan dalam payload UDP? (Petunjuk: jawaban untuk pertanyaan ini dapat ditentukan dari jawaban Anda untuk pertanyaan 2)
5. Berapa nomor port terbesar yang dapat menjadi port sumber? (Petunjuk: lihat petunjuk pada pertanyaan 4)
6. Berapa nomor protokol untuk UDP? Berikan jawaban Anda dalam notasi heksadesimal dan desimal. Untuk menjawab pertanyaan ini, Anda harus melihat ke bagian ”Protocol” pada datagram IP yang mengandung segmen UDP.
7. Periksa pasangan paket UDP di mana host Anda mengirimkan paket UDP pertama dan paket UDP kedua merupakan balasan dari paket UDP yang pertama. (Petunjuk: agar paket kedua merupakan balasan dari paket pertama, pengirim paket pertama harus menjadi tujuan dari paket kedua). Jelaskan hubungan antara nomor port pada kedua paket tersebut!

## Jawaban
1. Field UDP
![Lampiran](../assets/image/Modul%205%20(1).png)
Terdapat 4 field yang tersedia yaitu Source port, Destination port, Lenght, Checksum
2. Panjang setiap field yang tertera pada gambar di soal sebelumnya:
- Source port: 2 byte
- Destination port: 2 byte
- Lenght: 2 byte
- Checksum: 2 byte
UDP memiliki ukuran pasti yaitu 8 byte dan pada uji coba di atas tertera memiliki 4 field yang artinya masing - masing mendapatkan 2 byte

3. Lenght
![Lampiran](../assets/image/Modul%205%20(4).png)
Dari gambar tersebut dapat dilihat bahwa nilai Length adalah 58. Hal ini menunjukkan bahwa ukuran total UDP terdiri dari payload sebesar 50 byte ditambah header UDP sebesar 8 byte (50 + 8 = 58). Dengan demikian, field Length pada UDP merepresentasikan keseluruhan ukuran paket, yaitu gabungan antara header dan payload.

4. Jumlah Maksimum Byte UDP
Field Length pada UDP memiliki ukuran 16 bit (2 byte), sehingga nilai maksimum yang dapat direpresentasikan adalah:
2¹⁶ − 1 = 65.535 byte
Karena nilai Length mencakup header (8 byte) dan payload, maka:
Payload maksimum = 65.535 − 8 = 65.527 byte

5. Nomor Port Maksimum
Nomor port terbesar yang dapat digunakan sebagai source port pada UDP adalah 65.535. Hal ini disebabkan karena field port pada UDP menggunakan 16 bit, sehingga batas maksimal nilainya adalah 2¹⁶ − 1.

6. Analisis Field “Protocol” pada Header IP
![Lampiran](../assets/image/Modul%205%20(5).png)
Berdasarkan bagian Protocol pada header IP yang terlihat pada gambar (tertulis UDP (17)), dapat diketahui bahwa:
Nilai numerik untuk protokol UDP adalah 17 dalam bentuk desimal.
Jika dikonversikan ke dalam format heksadesimal, nilai tersebut menjadi 0x11.
Dengan demikian, field Protocol pada header IP digunakan untuk mengidentifikasi jenis protokol lapisan transport yang digunakan, dalam hal ini adalah UDP.

7. Hubungan port
![Lampiran](../assets/image/Modul%205%20(6).png)
![Lampiran](../assets/image/Modul%205%20(7).png)
Berdasarkan gambar yang ditampilkan:
Pada paket pertama (request), terlihat bahwa source port = 4334 dan destination port = 161.
Pada paket kedua (reply), nilainya menjadi source port = 161 dan destination port = 4334.
Hal ini menunjukkan bahwa nomor port pada paket kedua merupakan kebalikan dari paket pertama. Dengan kata lain, port asal pada paket pertama berubah menjadi port tujuan pada paket balasan, dan sebaliknya.
Dengan demikian, dapat disimpulkan bahwa dalam komunikasi UDP, ketika terjadi proses balasan, posisi port pengirim dan penerima akan saling bertukar mengikuti arah komunikasi yang berbalik.