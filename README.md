# REFLECTION

## [1] Commit 1 reflection notes
Ini adalah pertama kalinya saya menggunakan Rust. Menurut saya ini pengalaman yang menarik karena kita memulai project dengan menjalankan command `cargo new <nama_project>`, mirip seperti ketika menggunakan framework Django dan Spring Boot dimana start project dilakukan melalui command line interface (CLI). Menjalankan project juga dilakukan melalui CLI dengan menjalankan `cargo run`. Selain karena keunikan penggunaan CLI, saya juga mempelajari konsep baru dalam Rust yaitu ownership dimana setiap nilai dalam sebuah program memiliki hanya satu pemilik (owner) dalam satu waktu yang bertanggung jawab untuk mengurus memori terkait nilai tersebut. Pada tutorial kali ini, secara khusus di bagian satu ini, saya mempelajari pengembangan server web single-threaded menggunakan Rust. Pada bagian satu ini kita menyiapkan TCP listener untuk menerima koneksi masuk dan mencetak pesan sederhana saat terjadinya koneksi. Pada bagian kode yang ada, method handle_connection berfungsi untuk membaca HTTP request dan menyimpan requst tersebut dalam bentuk vektor untuk kemudian dicetak menggunakan `println!`.

## [2] Commit 2 reflection notes
Screenshot:
![commit2_screenshot](https://github.com/mariomichael/advprog-modul6/blob/main/images/commit2.png)
<br \>
Pada commit kedua ini, kita mengubah isi method handle_connection agar dapat menampilkan halaman HTML sederhana yang bisa dirender oleh browser. Untuk menampilkan halaman HTML tentu saja kita harus memiliki kode untuk halaman tersebut yang dalam tutorial kali ini dinamakan `hello.html` dan kode yang akan menampilkan file tersebut yang dalam tutorial ini bernama `main.rs`. Pada commit ini, terdapat beberapa perubahan seperti penggunaan modul fs untuk membaca isi file `hello.html`, pembuatan status line HTTP/1.1 200 OK, penambahan panjang konten dalam respons, dan pembentukan respons HTTP yang terdiri dari status line, panjang konten, dan konten HTML itu sendiri. Pada kode yang baru terdapat penambahan modul fs. Penambahan modul ini memungkinkan program untuk mengakses sistem file dan membaca isi file HTML. Setelah file HTML tersebut dibaca, isinya akan dimasukkan ke dalam variabel `contents`. Terdapat juga penambahan variabel length yang berisi keterangan mengenai panjang konten. Hal ini berfungsi untuk memberi tahu browser berapa banyak byte yang dikirim dalam response sehingga response dapat diproses dengan benar. Informasi mengenai panjang konten ini juga penting untuk menjaga stabilitas koneksi, manajemen memori, dan menjaga keamanan (seperti mencegah serangan Denial of Service (DoS)). Terakhir, dibuatlah response HTTP yang dibentuk menggunakan format string yang menggabungkan status line, panjang konten, dan isi konten HTML. Response ini akan dikirimkan kembali ke browser. Dengan adanya perubahan ini, server web dapat memberikan response dinamis berdasarkan konten dari file luar yang dalam kasus ini adalah `hello.html`.
