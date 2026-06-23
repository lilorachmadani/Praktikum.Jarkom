# MODUL 11 DHCP
DHCP (Dynamic Host Configuration Protocol) adalah protokol yang secara otomatis memberikan konfigurasi jaringan kepada perangkat yang terhubung, seperti IP address, subnet mask, gateway, dan DNS server. Dengan DHCP, pengguna tidak perlu melakukan pengaturan jaringan secara manual sehingga proses koneksi menjadi lebih mudah dan efisien.

Fungsi DHCP
* Memberikan alamat IP secara otomatis.
* Menyediakan konfigurasi jaringan yang dibutuhkan perangkat.
* Mempermudah pengelolaan jaringan.
* Mengurangi kesalahan saat pengaturan IP.

Kelebihan DHCP
* Konfigurasi jaringan lebih cepat dan mudah.
* Mengurangi risiko konflik alamat IP.
* Memudahkan penambahan perangkat baru.
* Pengelolaan alamat IP dapat dilakukan secara terpusat.

Kekurangan DHCP
* Bergantung pada server DHCP.
* Jika server bermasalah, klien tidak dapat memperoleh alamat IP.
* Memerlukan pengaturan server yang baik.
* Rentan terhadap penyalahgunaan jika keamanan jaringan kurang terjaga.

## DORA

**DORA (Discover, Offer, Request, Acknowledge)** adalah tahapan yang digunakan DHCP untuk memberikan alamat IP kepada klien. Klien terlebih dahulu mencari server DHCP melalui **Discover**, kemudian server memberikan penawaran alamat IP melalui **Offer**. Setelah itu klien mengirim **Request** untuk meminta alamat tersebut, dan server mengirim **Acknowledge (ACK)** sebagai konfirmasi bahwa alamat IP dapat digunakan.

## Langkah-Langkah

1. Unduh file **wireshark-traces.zip** kemudian ekstrak file tersebut.
2. Buka hasil ekstraksi menggunakan Wireshark.
3. Ketik **dhcp** pada kolom filter untuk menampilkan paket DHCP.
4. Amati proses DORA yang terjadi pada paket yang ditampilkan.
<img width="1173" height="602" alt="image" src="https://github.com/user-attachments/assets/f7417394-f82f-4951-9626-4bb65022ee38" />

## Proses DORA pada DHCP

**1. Discover**
* Klien mengirim pesan broadcast untuk mencari server DHCP yang aktif pada jaringan.

**2. Offer**
* Server DHCP membalas dengan menawarkan alamat IP beserta konfigurasi jaringan lainnya.

**3. Request**
* Klien memilih dan meminta alamat IP yang ditawarkan oleh server DHCP.

**4. Acknowledge (ACK)**
* Server mengonfirmasi permintaan tersebut dan mengizinkan klien menggunakan alamat IP yang diberikan.

