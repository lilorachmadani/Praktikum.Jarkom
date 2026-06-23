# MODUL 13 ARP

**ARP (Address Resolution Protocol)** adalah protokol yang digunakan untuk mencari dan mencocokkan **MAC Address** berdasarkan **IP Address** pada jaringan lokal. ARP memungkinkan perangkat mengirim data ke tujuan yang benar dengan mengetahui alamat fisik perangkat tujuan.

## Cara Kerja ARP

1. Perangkat mengetahui alamat IP tujuan, tetapi belum mengetahui MAC Address-nya.
2. Perangkat memeriksa ARP Cache untuk mencari informasi yang sudah tersimpan.
3. Jika tidak ditemukan, perangkat mengirim **ARP Request** ke seluruh jaringan.
4. Perangkat yang memiliki IP tujuan akan membalas dengan **ARP Reply** yang berisi MAC Address miliknya.
5. Informasi IP dan MAC Address disimpan ke dalam ARP Cache.
6. Setelah MAC Address diketahui, data dapat dikirim ke perangkat tujuan.

## Langkah-Langkah
1. Buka Command Prompt sebagai administrator, lalu jalankan perintah berikut untuk menghapus isi ARP Cache : arp -d *
   <img width="305" height="26" alt="image" src="https://github.com/user-attachments/assets/e8b5910a-0ae6-495a-956c-ae23f88612b0" />
2. Jalankan aplikasi Wireshark.
3. Pilih menu Analyze → Enabled Protocols, lalu pastikan IPv4 dalam keadaan aktif.
   <img width="1912" height="1021" alt="image" src="https://github.com/user-attachments/assets/f22eb283-a933-4465-bda0-596fb0d8bde0" />
4. Mulai proses capture pada interface jaringan yang digunakan.
5. Buka sebuah website melalui browser untuk menghasilkan aktivitas jaringan : http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html
6. Hentikan proses capture setelah website berhasil dimuat.
7. Ketik arp pada kolom filter Wireshark untuk menampilkan paket ARP.
   <img width="1918" height="276" alt="image" src="https://github.com/user-attachments/assets/44e78d72-ed3c-4546-8c47-7ee4124724e7" />
8. Pilih salah satu paket ARP untuk dianalisis.
    <img width="1917" height="1018" alt="image" src="https://github.com/user-attachments/assets/7e2ffe4d-bb6d-4906-859f-dba07a9cfd14" />

## Analisis Hasil
Berdasarkan hasil capture Wireshark, paket yang dipilih merupakan ARP Request dengan Opcode: request (1). Paket dikirim dari perangkat dengan alamat IP 192.168.0.1 dan MAC Address 40:ed:00:9c:f9:08 menuju alamat broadcast ff:ff:ff:ff:ff:ff.Pada kolom informasi terlihat pesan "Who has 192.168.0.111? Tell 192.168.0.1", yang menunjukkan bahwa perangkat dengan IP 192.168.0.1 sedang mencari MAC Address milik perangkat yang memiliki alamat IP 192.168.0.111. Karena alamat MAC tujuan belum diketahui, nilai Target MAC Address masih 00:00:00:00:00:00.Dari hasil tersebut dapat disimpulkan bahwa ARP digunakan untuk mencari alamat MAC berdasarkan alamat IP pada jaringan lokal. Setelah perangkat tujuan memberikan balasan ARP Reply, informasi tersebut akan disimpan pada ARP Cache sehingga komunikasi data dapat berlangsung dengan lebih cepat.
