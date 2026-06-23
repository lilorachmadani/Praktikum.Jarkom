# Modul 4 - DNS

## Nslookup
Merupakan perintah yang digunakan untuk mencari informasi DNS dari suatu domain. Dengan nslookup, kita bisa tahu alamat IP dari sebuah website, siapa server DNS yang menjawab, dan siapa nameserver resmi dari suatu domain.

### nslookup www.mit.edu
Digunakan untuk mencari alamat IP dari website MIT. Ketik nslookup www.mit.edu di Command Prompt

<img width="262" height="150" alt="image" src="https://github.com/user-attachments/assets/17ef9391-4f0d-4882-bcee-cf5e74d8c842" />

Ketika perintah dijalankan, DNS lokal kita yaitu tusbind.ac.id dengan alamat IP 10.217.7.77 yang menjawab. Hasilnya menunjukkan bahwa www.mit.edu sebenarnya diarahkan dulu ke nama lain yaitu e9566.dscb.akamaiedge.net, lalu baru mendapat alamat IP aslinya yaitu 23.217.163.122. Ada juga dua alamat IPv6 yang diberikan. Jawaban ini bersifat "Non-authoritative" artinya bukan langsung dari server resmi MIT, melainkan dari cache DNS lokal.

### nslookup -type=NS mit.edu
Digunakan untuk mencari nameserver (server DNS resmi) dari domain mit.edu. Nameserver adalah server yang paling tahu tentang semua informasi domain tersebut. Sama seperti tadi, ketik nslookup -type=NS mit.edu di Command Prompt

<img width="430" height="337" alt="image" src="https://github.com/user-attachments/assets/f4682e80-d562-4c4a-8a60-ec11bcefbd5f" />

DNS lokal tusbind.ac.id (10.217.7.77) merespons permintaan dengan memberikan 8 nameserver resmi milik MIT. Semua nameserver tersebut dikelola oleh Akamai, yaitu perusahaan penyedia layanan CDN (Content Delivery Network) yang besar. Selain itu, DNS juga memberikan alamat IP dari masing-masing nameserver tersebut. "Non-authoritative" karena diambil dari cache DNS lokal.

### nslookup www.aiit.or.kr bitsy.mit.edu
Meminta informasi IP dari www.aiit.or.kr langsung ke server bitsy.mit.edu (salah satu nameserver MIT). Tujuannya untuk membuktikan bahwa kita bisa bertanya ke server DNS tertentu, bukan hanya ke DNS lokal. Ketik nslookup www.aiit.or.kr bitsy.mit.edu di Command Prompt.

<img width="237" height="198" alt="image" src="https://github.com/user-attachments/assets/cee85154-3383-40af-8354-19fa0cbf6ecc" />

Percobaan pertama menampilkan pesan "Can't find server address for 'bitsy.mit.edu'", yang berarti nslookup tidak bisa menemukan alamat IP untuk bitsy.mit.edu. Namun, pencarian tetap dilanjutkan melalui DNS lokal dan akhirnya berhasil mendapatkan alamat IP dari www.aiit.or.kr. Pada percobaan kedua muncul pesan "DNS request timed out", yang berarti server bitsy.mit.edu tidak aktif atau tidak merespons permintaan. 

#### Pertanyaan 
- Jalankan nslookup untuk mendapatkan alamat IP dari server web di Asia. Berapa alamat IP 
server tersebut?
Menggunakan perintah nslookup www.aiit.or.kr (AIIT adalah institusi di Korea).
Alamat IP yang didapat: 104.21.74.8 dan 172.67.152.120
- Jalankan nslookup agar dapat mengetahui server DNS otoritatif untuk universitas di Eropa. 
Menggunakan perintah nslookup -type=NS mit.edu (MIT sebagai universitas di Amerika), hasilnya nameserver seperti eur5.akam.net yang berlokasi di Eropa dengan IP 23.74.25.64
- Jalankan nslookup untuk mencari tahu informasi mengenai server email dari Yahoo! Mail 
melalui salah satu server yang didapatkan di pertanyaan nomor 2. Apa alamat IP-nya? 
Berdasarkan perintah nslookup -type=MX yahoo.com 8.8.8.8, diperoleh mail server Yahoo yaitu mta5.am0.yahoodns.net. Setelah dilakukan pencarian alamat IP dengan perintah nslookup mta5.am0.yahoodns.net, diperoleh beberapa alamat IP, salah satunya adalah 98.136.96.75.


## Ipconfig
Merupakan  perintah bawaan Windows untuk melihat konfigurasi jaringan komputer, termasuk alamat IP, DNS server, dan informasi adapter lainnya. 

### ipconfig /all
Ketik ipconfig /all di Command Prompt.

<img width="592" height="426" alt="image" src="https://github.com/user-attachments/assets/5679a384-87bb-4813-a77b-3187d0833cb5" />

Digunakan untuk menampilkan semua informasi jaringan pada komputer. Dari hasilnya terlihat beberapa adapter jaringan yang terpasang. Pada praktikum ini, informasi yang paling penting adalah DNS Server lokal yang digunakan, yaitu tusbind.ac.id dengan IP 10.217.7.77, karena informasi tersebut akan dibandingkan dengan tujuan paket DNS yang tertangkap di Wireshark.

### ipconfig /displaydns
Ketik ipconfig /displaydns di Command Prompt.

<img width="392" height="442" alt="image" src="https://github.com/user-attachments/assets/1dcc70bc-d783-4f13-bdc7-f0d45a3c889d" />

Digunakan untuk menampilkan cache DNS yang tersimpan di komputer. Cache DNS adalah catatan dari hasil pencarian DNS sebelumnya, sehingga jika kita membuka domain yang sama lagi, komputer tidak perlu meminta alamat IP ke server DNS lagi.


## Tracing DNS dengan Wireshark

### Memfilter IP
Pertama, buka Wireshark dan pasang filter IP agar hanya menampilkan paket yang berasal dari atau menuju komputer. Lihat ip config pada ipconfig /all di IPv4 Address.
<img width="942" height="450" alt="image" src="https://github.com/user-attachments/assets/e4b2274a-c6f3-48c8-bba6-cec2fe01d354" />

Terdapat berbagai jenis paket tertangkap seperti UDP, TLS, TCP, dan QUIC. Ini adalah traffic normal yang berjalan di komputer.

### Membuka www.ietf.org
Setelah Wireshark berjalan, buka browser dan ketik http://www.ietf.org

<img width="942" height="437" alt="image" src="https://github.com/user-attachments/assets/e363bba8-d9b1-4e94-9e1c-4429b901c15e" />

Di balik ini, browser mengirim DNS query untuk mencari tahu IP dari www.ietf.org sebelum bisa terhubung ke server.

### Menganalisis Paket DNS di Wireshark
Untuk melihat khusus paket DNS yang berhubungan dengan ietf.org, gunakan filter: ip.addr == 10.218.15.227 && dns.qry.name contains "ietf", ketik di wireshark

<img width="940" height="485" alt="image" src="https://github.com/user-attachments/assets/70e4fc2d-e513-4130-97fc-9b16b7c83d94" />

Terlihat 4 paket DNS, terdiri dari 2 query dan 2 response untuk domain www.ietf.org.

#### Pertanyaan
- Cari pesan permintaan DNS dan balasannya. Apakah pesan tersebut dikirimkan melalui UDP 
atau TCP?   UDP. Terlihat di packet detail Wireshark pada paket no. 159: "User Datagram Protocol, Src Port: 60829, Dst Port: 53". DNS menggunakan UDP karena lebih ringan dan cepat untuk query sederhana.
- Apa port tujuan pada pesan permintaan DNS? Apa port sumber pada pesan balasannya?  Port tujuannya adalah 53 dan port sumbernya adalah 60829
- Pada pesan permintaan DNS, apa alamat IP tujuannya? Apa alamat IP server DNS lokal anda 
(gunakan ipconfig untuk mencari tahu)? Apakah kedua alamat IP tersebut sama?  IP tujuan DNS request: 10.217.7.77. DNS lokal dari ipconfig /all juga 10.217.7.77 (tusbind.ac.id). Ya, keduanya sama — query dikirim langsung ke DNS lokal
- Periksa pesan permintaan DNS. Apa “jenis” atau ”type” dari pesan tersebut? Apakah pesan 
permintaan tersebut mengandung ”jawaban” atau ”answers”?     Type: A (Standard query untuk mencari IPv4). Query tidak mengandung answers, di dalam paket query hanya ada bagian "Questions", belum ada jawaban.
- Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau ”answers” yang terdapat di 
dalamnya? Apa saja isi yang terkandung dalam setiap jawaban tersebut?    Terdapat 2 answers yaitu A 104.16.44.99 dan A 104.16.45.99. Terlihat di packet no. 160: "Standard query response... A www.ietf.org A 104.16.44.99 A 104.16.45.99"  
- Perhatikan paket TCP SYN yang selanjutnya dikirimkan oleh host Anda. Apakah alamat IP 
pada paket tersebut sesuai dengan alamat IP yang tertera pada pesan balasan DNS?     Ya. Setelah DNS reply memberikan IP 104.16.44.99 dan 104.16.45.99, paket berikutnya di Wireshark menuju ke salah satu IP tersebut untuk membangun koneksi TCP, membuktikan browser menggunakan hasil DNS untuk terkoneksi ke server IETF.
- alaman web yang sebelumnya anda akses (http://www.ietf.org) memuat beberapa 
gambar. Apakah host Anda perlu mengirimkan pesan permintaan DNS baru setiap kali ingin 
mengakses suatu gambar? Tidak selalu. Jika gambar berasal dari domain yang sama (ietf.org) yang sudah di-resolve, browser tidak perlu DNS query baru karena hasilnya sudah tersimpan di cache

### Menganalisis Paket DNS nslookup mit.edu di Wireshark
Untuk melihat paket DNS hasil nslookup mit.edu, gunakan filter: ip.addr == 10.218.15.227 && dns.qry.name contains "mit"

<img width="947" height="477" alt="image" src="https://github.com/user-attachments/assets/44bcea85-0d8e-4bf6-bdbc-6805a133123d" />

Terlihat paket DNS query dan response untuk domain mit.edu yang dikirim ke DNS lokal 10.217.7.77.

#### Pertanyaan
- Apa port tujuan pada pesan permintaan DNS? Apa port sumber pada pesan balasan DNS? Port tujuannya adalah 53 dan port sumbernya adalah 54720
- Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut merupakan default alamat IP server DNS lokal Anda? Request dikirim ke 10.217.7.77 (tusbind.ac.id). Ya, itu DNS lokal sesuai hasil ipconfig /all.
- Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan tersebut mengandung ”jawaban” atau ”answers”? Type: A (Standard query). Query tidak mengandung answers.
- Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau “answers” yang terdapat di dalamnya. Apa saja isi yang terkandung dalam setiap jawaban tersebut?  Balasan berisi CNAME + A record: Alias: www.mit.edu → e9566.dscb.akamaiedge.net, IP: 23.217.163.122 (IPv4), Dua alamat IPv6 tambahan (lupa ke skrinsyut)

### Memfilter DNS untuk nslookup -type=NS mit.edu di Wireshark
Setelah membuka wireshark dan memilih jaringan wifi, buka CMD dan ketik perintah nslookup -type=NS mit.edu di Command Prompt
<img width="263" height="145" alt="image" src="https://github.com/user-attachments/assets/3db7f912-bc0d-4bc1-ae13-812a1c79acb3" />

Setelah mematikan wireshark, gunakan filter dns untuk mengambil data dari Standard query (request) dan Standard query response dari NS mit.edu
<img width="951" height="482" alt="image" src="https://github.com/user-attachments/assets/87c73a5a-fcf7-4e0f-9cb9-1fb94881ca6b" />

#### Pertanyaan
- Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut 
merupakan default alamat IP server DNS lokal Anda? Permintaan DNS dikirim ke alamat IP: 2404:c0:b200::3:1. Ya, merupakan dns lokal yaitu tusbind.ac.id – 10.217.7.77
- Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan 
tersebut mengandung ”jawaban” atau ”answers”?

<img width="396" height="236" alt="image" src="https://github.com/user-attachments/assets/b72b5bd0-685f-4bc8-ab17-6c0ddaf67e2b" />

Dari situ terlihat bahwa:
Type = NS
Answer RRs = 0 (tidak mengandung jawaban)

- Periksa pesan balasan DNS. Apa nama server MIT yang diberikan oleh pesan balasan? 
Apakah pesan balasan ini juga memberikan alamat IP untuk server MIT tersebut? 
server MIT yang diberikan adalah:

<img width="426" height="215" alt="Screenshot 2026-04-05 131209" src="https://github.com/user-attachments/assets/5a9230c3-94a5-439e-a634-4cc03e5940ac" />

Pesan balasan juga memberikan alamat IP untuk server tersebut, contohnya:

<img width="567" height="92" alt="Screenshot 2026-04-05 131323" src="https://github.com/user-attachments/assets/a4e23e4f-5ed4-4cb9-b003-9be8de817a1f" />

### Menganalisis DNS Menggunakan Server www.aiit.or.kr bitsy.mit.edu
Setelah membuka wireshark dan memilih jaringan wifi, buka CMD dan ketik perintah nslookup www.aiit.or.kr bitsy.mit.edu di Command Prompt
<img width="226" height="202" alt="image" src="https://github.com/user-attachments/assets/0535fd8a-d358-474d-ad53-8f6d255528c3" />

Setelah mematikan wireshark, gunakan filter dns untuk mengambil data dari Standard query (request) dari www.aiit.or.kr

<img width="947" height="478" alt="image" src="https://github.com/user-attachments/assets/b9e96ace-ff2d-4369-91ff-cacbc6e8fc03" />

#### Pertanyaan
- Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut 
merupakan default alamat IP server DNS lokal Anda? Permintaan DNS dikirim ke alamat IP: 18.0.72.3. Bukan default DNS lokal, 18.0.72.3 adalah server tujuan domain yang diminta, bukan DNS lokal (sedang tidak memakai jaringan kampus).
- Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan 
tersebut mengandung ”jawaban” atau ”answers”? 

<img width="538" height="247" alt="Screenshot 2026-04-05 132625" src="https://github.com/user-attachments/assets/9507aa49-12c2-4d9a-94d7-8ee41dc70475" />

Di bagian Queries terlihat www.aiit.or.kr: type A, class IN artinya merupakan Type: A dan Digunakan untuk mencari alamat IPv4 dari domain. Serta terlihat Answer RRs: 0 yang berarti tidak ada jawaban dalam pesan query, karena ini adalah pesan permintaan (query) ke DNS server.

- Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau “answers” yang terdapat di 
dalamnya. Apa saja isi yang terkandung dalam setiap jawaban tersebut? 

<img width="235" height="202" alt="image" src="https://github.com/user-attachments/assets/7eed340d-f108-4d06-b316-fa24f285f239" />

Pada percobaan ini tidak terdapat jawaban (answers) karena server DNS tidak memberikan balasan dan terjadi DNS request timed out. Oleh karena itu informasi mengenai alamat IP atau server domain tidak dapat diperoleh dari query tersebut.
