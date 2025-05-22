## Experiment 2.1: Original code, and how it run

![alt text](image.png)

Output tersebut menunjukkan sistem chat real-time berbasis WebSocket di mana satu server (server.rs) menerima koneksi dari beberapa client (client.rs) dan mendistribusikan pesan yang diterima ke semua client lainnya menggunakan broadcast channel (tokio::sync::broadcast). Setiap client mengirim pesan ("beep boop", "beep boop from second client", "beepboop from third client") yang kemudian diterima oleh server dan diteruskan kembali ke semua client yang terhubung. Inilah sebabnya semua jendela terminal client mencetak output dari semua pesan yang dikirim oleh client lain, karena server berperan sebagai relay yang menyebarkan pesan ke seluruh peserta chat melalui broadcast.

## Experiment 2.2: Modifying port

![alt text](image-1.png)

Untuk memodifikasi port menjadi 8080 dan memastikan aplikasi WebSocket chat tetap berjalan dengan baik, kita perlu memastikan bahwa baik server maupun client terhubung pada port yang sama. Pada kode server, port ditentukan melalui TcpListener::bind("127.0.0.1:8080"), yang sudah menggunakan port 8080. Pada sisi client, URI WebSocket ditentukan melalui ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080")), yang juga sudah mengarah ke port 8080. Karena kedua sisi menggunakan protokol WebSocket (tokio_websockets) dan telah disesuaikan menggunakan port 8080, maka koneksi akan tetap berhasil selama tidak ada konflik port lain. 

## Experiment 2.3: Small changes, add IP and Port

![alt text](image-2.png)

Saya memodifikasi format pesan yang dikirim server ke setiap klien dengan menambahkan informasi pengirim, berupa IP dan port mereka. Sebelumnya, pesan hanya berisi teks yang diketik klien tanpa identitas pengirim yang jelas. Dengan penambahan informasi ini, setiap klien kini bisa mengetahui dari mana pesan berasal, walaupun belum ada fitur nama pengguna. Hal ini penting untuk membangun sistem komunikasi yang lebih informatif dan bisa dikembangkan lebih lanjut untuk fitur identitas seperti username. Hasil modifikasi ini bisa dilihat pada output konsol klien, di mana setiap pesan kini diawali dengan alamat IP dan port pengirim. Contohnya: From server: 127.0.0.1:63684 "bakekok from first client". 