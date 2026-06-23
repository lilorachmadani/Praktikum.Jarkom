# MODUL 12 : ICMP
## ICMP

**ICMP (Internet Control Message Protocol)** adalah protokol yang digunakan untuk mengirim informasi kontrol dan pesan kesalahan pada jaringan IP.

### Fungsi ICMP

- Mengecek koneksi jaringan.
- Mengetahui apakah host tujuan dapat dijangkau.
- Memberikan informasi jika terjadi kesalahan pengiriman data.

### Penggunaan ICMP

- **Ping** untuk menguji koneksi ke host tujuan.
- **Traceroute/Tracert** untuk melihat jalur paket data.
- Mengirim pesan error saat terjadi masalah jaringan.

### Hubungan ICMP dengan IP

ICMP bekerja bersama IP dengan membawa pesan kontrol dan informasi kesalahan dalam paket IP.

### Bagian Paket ICMP

- **Type** : Jenis pesan ICMP.
- **Code** : Detail dari jenis pesan.
- **Checksum** : Pengecekan kesalahan data.
- **Identifier** : Identitas paket.
- **Sequence Number** : Nomor urut paket.

## Analisis ICMP yang Dihasilkan Oleh Ping
1. Bukak wireshark dan pilih salah satu jaringan (Wifi), lalu aktifkan / capture
2. Buka CMD, kemudian ketikan perintah ping -n 10 www.ust.hk
   <img width="614" height="410" alt="image" src="https://github.com/user-attachments/assets/bab67e0f-7217-4704-af1a-dd967b95177d" />
3. Stop capture pada wireshark
4. Lakukan filter ICMP
5. Pilih dan expand salah satu paket ICMP Echo Request
6. Pilih dan expand salah satu paket ICMP Echo Reply

**Analisis**
- Pesan ICMP yang dihasilkan program Ping
  <img width="975" height="573" alt="image" src="https://github.com/user-attachments/assets/eb26212a-0d00-4c9d-ae52-3e19d02ddedd" />
  Program ping menghasilkan dua jenis pesan ICMP yaitu ICMP Echo Request dan ICMP Echo Reply. Pada percobaan ini, perintah di CMD (-n 10) menyatakan untuk melakukan 10 kali ping. Karena setiap ping menghasilkan 1 echo request dan 1 echo reply, maka total paket ICMP yang muncul di wireshark adalah 20 paket (10 request + 10 reply)
- Format dan Isi Pesan ICMP
  1. ICMP Echo Request
     <img width="975" height="269" alt="image" src="https://github.com/user-attachments/assets/458bc4b8-7b2e-4995-afb2-a9dfcb528fda" />
     - Type = 8 -> menandakan paket adalah Echo Request atau permintaan ping
     - Code = 0 -> menunjukkan tidak ada detail error tambahan pada pesan ICMP tersebut
     - Checksum = 0x4d4c [correct] -> checksum valid sehingga paket tidak mengalami kerusakan/error saat dikirim
     - Identifier = 1 (0x0001) -> digunakan sebagai penanda agar Echo Reply dapat dikenali sebagai balasan dari request yang sama
     - Sequence Number = 15 (0x000f) -> menunjukkan bahwa paket ini merupakan urutan ping ke-15 yang dikirim
  2. ICMP Echo Reply
     <img width="975" height="316" alt="image" src="https://github.com/user-attachments/assets/de75686f-3365-4d01-85e8-c103196f4a3e" />
     - Type = 0 -> menunjukkan bahwa paket merupakan Echo Reply atau balasan ping
     - Code = 0 -> tidak terdapat informasi tambahan atau error pada paket balasan
     - Checksum = 0x554c [correct] -> checksum valid sehingga paket reply diterima tanpa kerusakan data
     - Identifier = 1 (0x0001) -> identifier sama dengan paket request agar sistem dapat mencocokkan balasan dengan permintaan sebelumnya
     - Sequence Number = 15 (0x000f) -> menunjukkan bahwa paket reply ini merupakan balasan untuk paket request urutan ke-15

## Analisis ICMP yang Dihasilkan Oleh Traceroute
1. Bukak wireshark dan pilih salah satu jaringan (Wifi), lalu aktifkan / capture
2. Buka CMD, kemudian ketikan perintah tracert www.ust.hk
   <img width="632" height="402" alt="image" src="https://github.com/user-attachments/assets/904ca921-9e5a-4e7e-9ac0-4292b1d194e3" />
3. Stop capture pada wireshark
4. Lakukan filter ICMP
5. Pilih dan expand salah satu paket ICMP Echo Request
6. Pilih dan expand salah satu paket Time To Live (TTL)

**Analisis**
- Pesan ICMP yang dihasilkan oleh program tracerout
  <img width="1049" height="595" alt="image" src="https://github.com/user-attachments/assets/1009e434-c293-40ba-8274-bd6796660bb2" />
  1. ICMP Echo Request : Paket ini digunakan untuk meminta respon dari host atau router yang dilewati
  2. ICMP Time Exceeded (TTL Expired) : pesan yang dikirim oleh router ketika nilai TTL pada suatu paket habis sebelum paket mencapai tujuan
- Format dan Isi Pesan ICMP
  1. ICMP Echo Request
     
     <img width="726" height="226" alt="image" src="https://github.com/user-attachments/assets/0131eb7b-d0e1-4dab-938f-f96067ec4b48" />
     
     - Type = 8 -> menunjukkan paket merupakan Echo Request atau permintaan ping
     - Code = 0 -> tidak terdapat informasi tambahan/error pada paket
     - Checksum = 0xf7e5 [correct] -> checksum valid sehingga paket tidak mengalami kerusakan saat transmisi
     - Identifier = 1 (0x0001) -> digunakan sebagai penanda paket request
     - Sequence Number = 25 (0x0019)-> menunjukkan bahwa paket ini merupakan paket urutan ke-25
  2. ICMP Time Exceeded
     <img width="1049" height="329" alt="image" src="https://github.com/user-attachments/assets/5c8379a3-3d95-42ae-8499-9b2bd46ad149" />
     - Type = 11 -> menunjukkan paket merupakan Time Exceeded
     - Code = 0 -> berarti TTL exceeded in transit, yaitu TTL habis di perjalanan
     - Checksum = 0xf4ff [correct] -> menandakan paket diterima tanpa error
     - Source IP = 10.218.0.253 -> router yang mengirim pesan TTL exceeded
     - Destination IP = 10.218.10.188 -> Host pengirim traceroute
     
