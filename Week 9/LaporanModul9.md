# Modul 9 Web Server

Web server adalah perangkat lunak yang menerima permintaan dari browser dan mengirimkan halaman atau data yang diminta pengguna melalui protokol HTTP atau HTTPS. Fungsi utamanya adalah menyimpan, mengelola, dan menyediakan konten website, seperti halaman HTML, gambar, dan video. Contoh web server yang umum digunakan yaitu Apache, Nginx, dan Microsoft IIS.

## Langkah-Langkah 
1. Buat sebuah file Python menggunakan VS Code.
2. Salin dan tempel kode program server ke dalam file tersebut.
```python
from socket import *#ambil semua fungsi dari library socket
import threading#buat jalanin banyak client sekaligus

def handle_client(connectionSocket):#fungsi buat ngelayanin client
    try:
        message = connectionSocket.recv(1024).decode()#terima request dari browser
        message = message[4:16]#ambil nama file yang diminta
        print(message)#tampilin nama file di terminal

        f = open(message[1:])#buka file yang diminta client
        outputData = f.read()#baca isi file

        connectionSocket.send(
            "HTTP/1.1 200 OK\r\n\r\n".encode()#kasih status kalau file berhasil ditemukan
        )

        connectionSocket.sendall(outputData.encode())#kirim isi file ke browser

        connectionSocket.close()#tutup koneksi kalau sudah selesai
    
    except IOError:#kalau file tidak ada
        connectionSocket.send(
            "HTTP/1.1 404 Not Found\r\n\r\n".encode()#kirim status error 404
        )

        connectionSocket.send(
            "<h1>404 Not found</h1>".encode()#tampilin pesan file tidak ditemukan
        )

        connectionSocket.close()#tutup koneksi

serverSocket = socket(AF_INET, SOCK_STREAM)#buat socket TCP
serverSocket.bind(('', 6789))#jalan di port 6789
serverSocket.listen(5)#siap nerima koneksi client

print("[SYSTEM] server is running...")#info kalau server sudah aktif

while True:#biar server terus jalan
    connectionSocket, addr = serverSocket.accept()#terima koneksi dari client

    thread = threading.Thread(#buat thread baru untuk setiap client
        target=handle_client,
        args=(connectionSocket,)
    )

    thread.start()#jalankan threadnya
```
3. Buat file HTML baru pada direktori yang sama dengan file Python.
4. Masukkan kode HTML yang telah disediakan ke dalam file HTML tersebut.
```html
<html>
<head>
    <title>eak</title>
</head>
<body>
    <h1>awokawok berhasil</h1>
</body>
</html>
```
4. Jalankan program Python terlebih dahulu agar server aktif.
5. Setelah server berjalan, buka browser dan akses alamat http://localhost:6789/index.html untuk melihat halaman HTML yang ditampilkan oleh server.
<img width="1192" height="637" alt="image" src="https://github.com/user-attachments/assets/1fb83ffa-4597-4629-85c3-7199161fdc33" />


