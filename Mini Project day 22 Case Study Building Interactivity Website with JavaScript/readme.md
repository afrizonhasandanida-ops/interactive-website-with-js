# Mini Project: Building Interactivity Website with JavaScript (Atelier Audio)

Proyek ini merupakan lanjutan dari **Study Case Phase 1** yang berfokus pada penerapan manipulasi DOM, *event handling*, validasi input interaktif, serta pengelolaan *asynchronous* JavaScript menggunakan Vanilla JavaScript, HTML, dan CSS.

---

##  Deskripsi Halaman

Proyek ini mempertahankan dua checkpoint halaman detail produk dari fase sebelumnya:
1. **Halaman Produk 1 (Hardcoded - `index.html`)**
   - Menampilkan detail produk utama (*MW75 Custom Wireless ANC Headphones*) menggunakan data statis (*hardcoded*) untuk nama produk, harga dasar, stok, galeri gambar, deskripsi, dan pilihan warna.
   - Mendukung interaksi langsung pada variasi warna, opsi *custom engraving*, perubahan kuantitas, dan kalkulasi subtotal secara dinamis.

2. **Halaman Produk 2 (API-Driven)**
   - Mengambil dan merender data produk kedua secara asinkron dari *endpoint* API *baseline* yang telah disiapkan pada Phase 1.
   - Mengelola siklus hidup *request* secara lengkap: menampilkan indikator *loading* saat memuat data, merender konten saat sukses, dan menampilkan pesan error yang informatif apabila jaringan bermasalah atau *response* HTTP gagal (`!response.ok`).

---

##  Fitur Interaksi yang Diimplementasikan

- **Pemilihan Variasi & Galeri Produk**: Mengubah warna produk (*Matte Black*, *Gunmetal*, *Silver*) akan memperbarui label warna aktif, gambar utama, dan status thumbnail secara sinkron.
- **Personalisasi (Custom Engraving)**: Mengaktifkan opsi *engraving* akan membuka kolom input teks (maksimal 12 karakter alfanumerik), menampilkan *live preview* pada visual produk, serta menambahkan biaya personalisasi ke total harga.
- **Kontrol & Validasi Kuantitas**:
  - Tombol tambah (`+`) dan kurang (`-`) menggunakan `addEventListener`.
  - Validasi ketat memastikan kuantitas selalu berupa **bilangan bulat positif** (minimal `1`), menolak angka `0`, negatif, desimal, serta membatasi jumlah maksimal sesuai stok total yang tersedia (`5` unit).
- **Kalkulasi Subtotal Real-time & Konfirmasi Pesanan**:
  - Memperbarui tampilan subtotal otomatis melalui `textContent` setiap kali terjadi perubahan kuantitas atau opsi *engraving*.
  - Menekan tombol **Konfirmasi Pesanan** akan memvalidasi ulang input, menampilkan ringkasan pesanan pada layar, serta memperbarui status interaksi lokal.
- **Asynchronous Data Fetching & Error Handling (Halaman API)**:
  - Menggunakan `fetch` dengan pengecekan `response.ok` sebelum memparsing JSON.
  - Menghilangkan indikator *loading* baik saat request berhasil maupun gagal, serta mencegah pemasangan *event listener* atau *request* duplikat.

---

## 🔗 Endpoint Baseline

- **Halaman Produk 1**: Menggunakan objek data lokal statis pada `script.js` (`{ stock: 5, price: 8999000 }`).
- **Halaman Produk 2**: Menggunakan *endpoint* API *baseline* dari Study Case Phase 1 tanpa menyimpan kredensial sensitif maupun API key di sisi *frontend* atau repositori.

---

##  Cara Menjalankan Proyek

1. **Clone atau unduh repositori ini** ke komputer lokal Anda:
   ```bash
   git clone <url-repository-github-anda>
   ```
2. Buka folder proyek menggunakan **Visual Studio Code**.
3. Jalankan proyek menggunakan ekstensi **Live Server** (klik kanan pada `index.html` lalu pilih **Open with Live Server**) atau buka langsung file `index.html` melalui browser modern (Chrome, Edge, Firefox).
4. Untuk menguji halaman kedua (API-Driven), pastikan koneksi internet aktif atau *server baseline* berjalan sesuai konfigurasi Phase 1.

---

##  Cara Menguji & Tabel Skenario Pengujian

Pengujian dilakukan langsung pada browser untuk memverifikasi interaksi DOM, validasi kuantitas, dan penanganan proses asinkron.

| No | Skenario Pengujian | Input / Kondisi | Expected Result | Actual Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Pemilihan variasi warna | Klik tombol warna *Gunmetal* atau *Silver* | Teks warna berubah, gambar utama berganti sesuai warna, dan thumbnail aktif menyesuaikan. | Teks warna, gambar produk, dan status thumbnail ter-update dengan akurat. | Berhasil |
| 2 | Fitur *Custom Engraving* & subtotal | Centang *Tambah Engraving* lalu ketik teks `ADI 2026` | Kolom input aktif, teks tampil pada *preview* headphone, dan subtotal bertambah Rp350.000. | Input aktif, pratinjau muncul pada gambar, dan total harga bertambah sesuai tarif. | Berhasil |
| 3 | Kuantitas valid & kalkulasi subtotal | Klik tombol `+` hingga kuantitas bernilai `3` | Nilai kuantitas menjadi `3`, subtotal otomatis terhitung (`Harga Satuan × 3`). | Kuantitas dan subtotal tampil sesuai perhitungan pada UI. | Berhasil |
| 4 | Validasi kuantitas minimum & negatif | Klik tombol `-` saat kuantitas bernilai `1` atau input nilai `0` / negatif / desimal | Tombol `-` nonaktif pada angka `1`; nilai di bawah `1` atau pecahan otomatis ditolak/disesuaikan. | Input tidak valid ditolak dan kuantitas tetap terjaga sebagai bilangan bulat positif (`>= 1`). | Berhasil |
| 5 | Validasi batas stok maksimum | Klik tombol `+` terus-menerus melebihi stok (`5`) | Kuantitas berhenti di angka `5` dan tombol `+` menjadi nonaktif (`disabled`). | Kuantitas tertahan pada batas stok maksimal (`5`) dan tombol `+` nonaktif. | Berhasil |
| 6 | Konfirmasi pesanan valid | Pilih warna, atur kuantitas valid, lalu klik **Konfirmasi Pesanan** | Muncul pesan rincian pesanan berisi warna, status engraving, kuantitas, dan total harga. | Kotak konfirmasi muncul dengan detail pesanan yang sesuai. | Berhasil |
| 7 | Memuat data halaman API | Buka halaman produk kedua (API-Driven) | Indikator *loading* tampil terlebih dahulu, lalu data produk dirender setelah response sukses. | Loading muncul singkat dan data produk tampil lengkap setelah fetch selesai. | Berhasil |
| 8 | Penanganan error request API | Putuskan koneksi internet / ubah endpoint menjadi tidak valid lalu muat ulang | Indikator *loading* hilang dan pesan *error state* ditampilkan tanpa *request* berulang. | Loading berhenti dan pesan kesalahan tampil jelas pada halaman. | Berhasil |

---

##  Catatan Penggunaan AI

Dalam pengerjaan proyek ini, AI digunakan secara terbatas sebagai asisten diskusi untuk meninjau struktur validasi kuantitas pada JavaScript, memastikan kesesuaian logika *event handling* (`addEventListener` dan `textContent`), serta menyusun format dokumentasi. Seluruh kode telah diuji dan diverifikasi secara manual pada browser.
