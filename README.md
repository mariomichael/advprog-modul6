# REFLECTION

## [1] Commit 1 reflection notes
Ini adalah pertama kalinya saya menggunakan Rust. Menurut saya ini pengalaman yang menarik karena kita memulai project dengan menjalankan command `cargo new <nama_project>`, mirip seperti ketika menggunakan framework Django dan Spring Boot dimana start project dilakukan melalui command line interface (CLI). Menjalankan project juga dilakukan melalui CLI dengan menjalankan `cargo run`. Selain karena keunikan penggunaan CLI, saya juga mempelajari konsep baru dalam Rust yaitu ownership dimana setiap nilai dalam sebuah program memiliki hanya satu pemilik (owner) dalam satu waktu yang bertanggung jawab untuk mengurus memori terkait nilai tersebut. Pada tutorial kali ini, secara khusus di bagian satu ini, saya mempelajari pengembangan server web single-threaded menggunakan Rust. Pada bagian satu ini kita menyiapkan TCP listener untuk menerima koneksi masuk dan mencetak pesan sederhana saat terjadinya koneksi. Pada bagian kode yang ada, method handle_connection berfungsi untuk membaca HTTP request dan menyimpan requst tersebut dalam bentuk vektor untuk kemudian dicetak menggunakan `println!`.

## [2] Commit 2 reflection notes
Screenshot:
![commit2_screenshot](https://github.com/mariomichael/advprog-modul6/blob/main/images/commit2.png)
Pada commit kedua ini, kita mengubah isi method handle_connection agar dapat menampilkan halaman HTML sederhana yang bisa dirender oleh browser. Untuk menampilkan halaman HTML tentu saja kita harus memiliki kode untuk halaman tersebut yang dalam tutorial kali ini dinamakan `hello.html` dan kode yang akan menampilkan file tersebut yang dalam tutorial ini bernama `main.rs`. Pada commit ini, terdapat beberapa perubahan seperti penggunaan modul fs untuk membaca isi file `hello.html`, pembuatan status line HTTP/1.1 200 OK, penambahan panjang konten dalam respons, dan pembentukan respons HTTP yang terdiri dari status line, panjang konten, dan konten HTML itu sendiri. Pada kode yang baru terdapat penambahan modul fs. Penambahan modul ini memungkinkan program untuk mengakses sistem file dan membaca isi file HTML. Setelah file HTML tersebut dibaca, isinya akan dimasukkan ke dalam variabel `contents`. Terdapat juga penambahan variabel length yang berisi keterangan mengenai panjang konten. Hal ini berfungsi untuk memberi tahu browser berapa banyak byte yang dikirim dalam response sehingga response dapat diproses dengan benar. Informasi mengenai panjang konten ini juga penting untuk menjaga stabilitas koneksi, manajemen memori, dan menjaga keamanan (seperti mencegah serangan Denial of Service (DoS)). Terakhir, dibuatlah response HTTP yang dibentuk menggunakan format string yang menggabungkan status line, panjang konten, dan isi konten HTML. Response ini akan dikirimkan kembali ke browser. Dengan adanya perubahan ini, server web dapat memberikan response dinamis berdasarkan konten dari file luar yang dalam kasus ini adalah `hello.html`.

## [3] Commit 3 reflection notes
Screenshot:
![commit3_screenshot](https://github.com/mariomichael/advprog-modul6/blob/main/images/commit3.png)
Pada commit ketiga ini, kita menambahkan case halaman HTML jika server merespon bahwa halaman yang direquest tidak tersedia. Hal ini dilakukan dengan menambahkan halaman `bad.html` pada opsi respon yang terdapat di `main.rs`. Halaman `bad.html` akan berisi konten HTML yang menyatakan bahwa halaman yang direquest tidak tersedia. Hal ini dilakukan dengan menambahkan if-else berdasarkan hasil request_line. Jika hasilnya "GET / HTTP/1.1", berarti request berhasil dan akan ditampilkan halaman `hello.html`, namun jika tidak, akan ditampilkan halaman error seperti`bad.html`. Pada kode dilakukan refactoring untuk menghilangkan bagian kode yang ada pengulangan (di bagian if-else) sehingga kode menjadi lebih efisien dan mudah dimengerti.

## [4] Commit 4 reflection notes
Pada commit keempat ini, kita memodifikasi method `handle_connection` untuk memberikan simulasi delay selama beberapa detik. Hal ini biasa dilakukan jika server sedang menangani request dengan jumlah yang banyak secara single-threaded. Oleh karena itu kita dapat menggunakan ThreadPool untuk menghandle request yang banyak secara bersamaan dengan lebih baik sehingga pengguna tidak perlu merasakan delay seperti yang disimulasikan dalam commit kali ini. Dalam commit ini sendiri, jika URL nya ditulis seperti biasa tanpa menambahkan apa-apa, halaman akan terbuka secara langsung dengan cepat. Namun jika kita menambahkan `/sleep` pada request, maka otomatis akan ada delay yang diberikan sesuai kondisional yang sudah disetting sebelumnya. Dengan menggunakan teknologi ThreadPool, yaitu teknologi agar sebuah web dapat menghandle berbagai thread secara simultan, masalah ini bisa diselesaikan. 

## [5] Commit 5 reflection notes
Pada commit kelima ini kita menerapkan konsep multi-threading dengan menggunakan ThreadPool. ThreadPool ini sendiri adalah kumpulan thread yang dipanggil dan menunggu untuk mengeksekusi sebuah tugas. Dengan menggunakan teknologi ini, browser dapat membagi tugas oleh banyak request yang diberikan olehnya ke dalam beberapa thread. Ketika mendapat tugas baru, program akan mengassign satu per satu thread untuk mengerjakan tugas tersebut. Hal ini berlaku untuk tugas selanjutnya. Setelah tugas selesai dikerjakan suatu thread, thread tersebut akan kembali tersedia. Ini membantu web menghandle makin banyak request satu waktu.

// add comment for rewriting commit message (5) Multithreaded server using Threadpool