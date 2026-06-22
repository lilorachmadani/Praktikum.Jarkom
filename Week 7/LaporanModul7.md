__________________________________________

# Modul 7 - SOCKET PROGRAMMING

## penjelasan socket
Socket programming adalah metode komunikasi antar komputer dalam jaringan menggunakan socket sebagai penghubung. Terdapat dua peran utama, yaitu client yang mengirim data dan server yang menerima serta merespons data. Komunikasi dapat menggunakan protokol TCP yang andal atau UDP yang lebih cepat namun tanpa jaminan pengiriman. Dengan demikian, socket programming memungkinkan pertukaran data secara langsung antar perangkat dalam jaringan.

# implementasi TCP

## TCP Client
```python
from socket import *  # memanggil seluruh fungsi yang ada pada library socket

serverName = "localhost"  # host tujuan yang akan dihubungi
serverPort = 12000  # nomor port yang digunakan server

clientSocket = socket(AF_INET, SOCK_STREAM)  # membuat socket berbasis IPv4 dan protokol TCP
clientSocket.connect(
    (serverName, serverPort)
)  # melakukan koneksi ke server yang ditentukan

print("[SYSTEM] Masukan pesan")  # menampilkan instruksi kepada pengguna

running = True  # penanda agar program tetap berjalan
while running:  # perulangan utama client
    message = input("> ")  # membaca pesan dari keyboard
    
    # mengirim data ke server setelah diubah menjadi format byte
    clientSocket.send(message.encode())

    if message == "exit":  # jika pengguna mengetik exit
        print("[SYSTEM] keluar dari program")
        running = False  # menghentikan proses perulangan
        break

    modifiedMessage = clientSocket.recv(2048)  # menerima balasan dari server dengan buffer 2048 byte

    # menampilkan pesan yang diterima setelah dikonversi kembali ke string
    print("[SERVER] pesan : ", modifiedMessage.decode())

clientSocket.close()  # mengakhiri koneksi socket
print("[SYSTEM] socket ditutup")  # konfirmasi bahwa koneksi telah ditutup
```
## TCP server
```python
from socket import *  # memuat seluruh fungsi yang tersedia pada modul socket

serverPort = 12000  # menentukan port yang akan dipakai server

serverSocket = socket(AF_INET, SOCK_STREAM)  # membuat endpoint komunikasi TCP berbasis IPv4
serverSocket.bind(("", serverPort))  # mengaitkan socket dengan port yang telah ditentukan
serverSocket.listen(1)  # mengaktifkan mode listening untuk menerima permintaan koneksi

print(f"[SYSTEM] Server berjalan pada port {serverPort}")  # menampilkan status server
print("[SYSTEM] Menunggu koneksi client...")  # memberi tahu bahwa server siap menerima koneksi

connectionSocket, addr = serverSocket.accept()  # menerima koneksi yang masuk dari client

print(f"[CLIENT] Terhubung dari {addr}")  # menampilkan alamat client yang berhasil tersambung

running = True  # flag untuk mengendalikan jalannya program

while running:  # perulangan selama server masih aktif

    message = connectionSocket.recv(2048).decode()  # membaca data dari client dan mengubahnya menjadi teks

    if not message:  # memeriksa apakah tidak ada data yang diterima
        break  # menghentikan loop jika koneksi terputus

    print("[CLIENT] pesan :", message)  # mencetak pesan yang dikirim client ke terminal

    if message.lower() == "exit":  # mengecek apakah client ingin mengakhiri sesi
        print("[SYSTEM] Client keluar")  # notifikasi bahwa client telah keluar
        running = False  # mengubah status agar loop berhenti
        break

    reply = f"Pesan diterima: {message}"  # menyusun pesan balasan untuk client

    connectionSocket.send(reply.encode())  # mengirim respons ke client dalam format byte

connectionSocket.close()  # menutup koneksi dengan client
serverSocket.close()  # menghentikan layanan server dan menutup socket

print("[SYSTEM] Server ditutup")  # menampilkan informasi bahwa server telah berhenti
```

## Alur TCP
1. Server dijalankan terlebih dahulu
2. Client melakukan koneksi ke server
3. Client mengirim data
4. Server memproses data
5. Server mengirim hasil ke client
6. Client menampilkan hasil
7. Jika kita ketik exit kita akan keluar dan server berhenti

### Output

# Implementasi UDP

## UDP Client
```python
from socket import *  # memanggil seluruh fungsi dari modul socket

serverName = 'localhost'  # host server yang akan dihubungi
serverPort = 12000  # nomor port tempat server berjalan

clientSocket = socket(AF_INET, SOCK_DGRAM)  # membuat socket UDP menggunakan IPv4

print("[SYSTEM] Masukkan pesan (ketik 'exit' untuk keluar)\n")  # menampilkan petunjuk penggunaan

while True:  # menjalankan program secara berulang hingga dihentikan

    message = input("> ")  # membaca pesan yang dimasukkan pengguna

    if not message:  # memeriksa apakah input kosong
        continue  # kembali ke awal perulangan tanpa mengirim data

    clientSocket.sendto(
        message.encode(),  # mengubah teks menjadi format byte sebelum dikirim
        (serverName, serverPort)  # menentukan alamat tujuan pengiriman
    )

    if message.lower() == 'exit':  # mengecek perintah untuk mengakhiri program
        print("[SYSTEM] Keluar dari program.")  # notifikasi bahwa client akan berhenti
        break  # keluar dari loop utama

    balasan, _ = clientSocket.recvfrom(2048)  # menerima paket data dari server
                                              # kapasitas maksimum data yang diterima adalah 2048 byte

    print(f"[SERVER] pesan: {balasan.decode()}\n")  # menampilkan isi balasan dari server

clientSocket.close()  # melepaskan resource socket yang digunakan

print("[SYSTEM] Socket ditutup.")  # informasi bahwa koneksi client telah berakhir
```
## UDP Server
```python
from socket import *  # mengimpor seluruh fungsi yang tersedia pada modul socket

serverPort = 12000  # menentukan port yang akan digunakan untuk menerima koneksi

serverSocket = socket(AF_INET, SOCK_DGRAM)  # membuat socket UDP berbasis IPv4
serverSocket.bind(("", serverPort))  # menghubungkan socket ke port yang telah ditentukan

print(f"[SYSTEM] Server UDP berjalan di port {serverPort}")  # menampilkan status server
print("[SYSTEM] Menunggu pesan dari client...\n")  # memberi informasi bahwa server siap menerima data

running = True  # penanda apakah server masih aktif

while running:  # menjalankan server secara terus-menerus

    message, clientAddress = serverSocket.recvfrom(2048)  # menerima paket data beserta alamat pengirim
    message = message.decode()  # mengubah data byte menjadi teks yang dapat dibaca

    print(f"[CLIENT {clientAddress}] pesan: {message}")  # menampilkan isi pesan dan alamat pengirim

    if message.lower() == "exit":  # memeriksa apakah client mengirim perintah keluar
        print("[SYSTEM] Client keluar.")  # menampilkan notifikasi penghentian koneksi
        running = False  # mengubah status agar perulangan berhenti
        break

    balasan = f"Pesan diterima: {message}"  # menyiapkan respons untuk dikirim kembali

    serverSocket.sendto(
        balasan.encode(),  # mengubah teks balasan menjadi byte
        clientAddress  # mengirim balasan ke alamat client yang sesuai
    )

serverSocket.close()  # menonaktifkan socket server

print("[SYSTEM] Server ditutup.")  # menampilkan pesan bahwa server sudah berhenti
```

## Alur UDP
1. Server dijalankan
2. Client langsung mengirim data tanpa koneksi
3. Server menerima data
4. Server memproses
5. Server mengirim balasan
6. Client menerima hasil
7. Jika kita ketik exit kita akan keluar dan server berhenti

### Output

