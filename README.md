## Experiment 2.1: Original code, and how it run

![alt text](image.png)

Output tersebut menunjukkan sistem chat real-time berbasis WebSocket di mana satu server (server.rs) menerima koneksi dari beberapa client (client.rs) dan mendistribusikan pesan yang diterima ke semua client lainnya menggunakan broadcast channel (tokio::sync::broadcast). Setiap client mengirim pesan ("beep boop", "beep boop from second client", "beepboop from third client") yang kemudian diterima oleh server dan diteruskan kembali ke semua client yang terhubung. Inilah sebabnya semua jendela terminal client mencetak output dari semua pesan yang dikirim oleh client lain, karena server berperan sebagai relay yang menyebarkan pesan ke seluruh peserta chat melalui broadcast.