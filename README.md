# 🏪 Bizmart UMKM — Web App

> Platform Digital untuk Pelaku UMKM Indonesia  
> Daily Project 7 — Rekayasa Kebutuhan D

**Nama:** Kurnia Nurhajijah  
**NIM:** 202310370311260  
**Kelas:** Rekayasa Kebutuhan D

---

## 🚀 Tentang Aplikasi

**Bizmart UMKM** adalah platform web terintegrasi yang dirancang khusus untuk mendukung pelaku Usaha Mikro, Kecil, dan Menengah (UMKM) di Indonesia. Aplikasi ini dikembangkan berdasarkan desain dari Daily Project 6.

### Fitur Utama

| Fitur | Deskripsi |
|-------|-----------|
| 🔐 Login & Register | Autentikasi pengguna dengan role Admin & User; register wajib email berformat valid (mis. `email@gmail.com`) dan password min. 6 karakter, peringatan tampil di form jika tidak sesuai |
| 🔑 Lupa & Reset Password | Verifikasi email → kode reset 6 digit (berlaku 10 menit, maks. 5 percobaan) → password baru + konfirmasi |
| 🔒 Password Anti-Salin | Semua field password memblokir copy/cut |
| 🛍️ Smart Catalog | Katalog produk UMKM dengan filter kategori & pencarian |
| 🛒 Keranjang Belanja | Manajemen cart real-time dengan update qty |
| 📦 Tracking Pesanan | Pelacakan status pesanan step-by-step |
| ❌ Pembatalan Pesanan | Pelanggan dapat membatalkan pesanan berstatus Menunggu/Diproses; stok otomatis dikembalikan |
| ⭐ Ulasan & Rating Produk | Pelanggan memberi rating & komentar untuk produk dari pesanan yang sudah Selesai; rata-rata rating tampil di katalog |
| 📊 Admin Dashboard | Ringkasan statistik, grafik tren pendapatan & produk terlaris, dan pesanan terbaru |
| ⚙️ CRUD Produk | Tambah, edit, hapus produk (Admin) |
| 📋 Manajemen Pesanan | Update status pesanan (Admin) |
| 👥 Manajemen User | Kelola pengguna platform (Admin) |
| 📱 Responsif | Tampilan optimal di desktop, tablet, dan mobile |

### 🆕 Detail Fitur Tambahan

**0. Autentikasi (diperbarui)**
- **Akun user demo dihapus.** Satu-satunya akun bawaan adalah admin (`admin@bizmart.id`). User harus mendaftar sendiri lewat tab *Daftar*.
- **Validasi register:** email harus berformat `nama@domain.tld` (contoh `email@gmail.com`), password minimal 6 huruf/angka (karakter bebas). Pelanggaran memunculkan peringatan merah di bawah field + toast.
- **Lupa password:** klik *Lupa password?* → isi email terdaftar → kode reset 6 digit dibuat → isi kode + password baru + konfirmasi.
- **Catatan:** karena aplikasi tanpa backend, pengiriman email **disimulasikan**: kode ditampilkan di layar. Untuk produksi, kirim kode lewat layanan email di server.
- **Password tidak bisa disalin:** event copy/cut pada field password diblokir (paste tetap diperbolehkan agar kompatibel dengan password manager).
- **Migrasi data:** saat pertama kali dibuka dengan versi ini, user lama di `localStorage` (beserta pesanan & ulasannya) dibersihkan, admin dipertahankan.

**1. Riwayat & Pembatalan Pesanan (Pelanggan)**
- Tombol "Batalkan Pesanan" tampil pada pesanan berstatus *Menunggu Konfirmasi* atau *Sedang Diproses*.
- Saat dibatalkan: status berubah menjadi *Dibatalkan*, stok produk terkait dikembalikan otomatis, dan pesanan dikeluarkan dari perhitungan pendapatan admin.
- Konfirmasi dialog mencegah pembatalan tidak sengaja.

**2. Ulasan & Rating Produk**
- Tombol "Beri Ulasan" muncul per item produk pada pesanan berstatus *Selesai*, dan hanya bisa diisi satu kali per item pesanan.
- Ulasan berisi rating bintang (1–5) dan komentar wajib diisi.
- Rata-rata rating & jumlah ulasan tampil di kartu produk pada halaman Toko; pelanggan dapat membuka daftar ulasan lengkap suatu produk.

**3. Grafik Statistik Admin Dashboard**
- **Tren Pendapatan**: grafik batang pendapatan per tanggal transaksi (maks. 7 titik data terbaru, pesanan dibatalkan tidak dihitung).
- **Produk Terlaris**: grafik batang 5 produk dengan jumlah unit terjual terbanyak.
- Grafik dibangun native dengan HTML/CSS (tanpa library eksternal) agar tetap ringan dan sesuai arsitektur single-file aplikasi.

---

## 🧪 Pengujian Kualitas Aplikasi

Pengujian dilakukan sesuai aspek kualitas perangkat lunak berdasarkan desain Daily Project 6.

### 1. Pengujian Fungsionalitas (Functionality Testing)

| No | Skenario Uji | Input | Output yang Diharapkan | Hasil | Status |
|----|-------------|-------|----------------------|-------|--------|
| F-01 | Login admin dengan kredensial valid | Email & password akun ber-role Admin | Masuk ke halaman Dashboard Admin | Berhasil masuk ke Dashboard Admin | ✅ PASS |
| F-02 | Login user dengan kredensial valid | Email & password akun ber-role User | Masuk ke halaman Toko | Berhasil masuk ke halaman Toko | ✅ PASS |
| F-03 | Login dengan kredensial salah | Email: salah@email.com, Password: salah | Muncul pesan error "Email atau password salah!" | Toast error muncul, tidak bisa masuk | ✅ PASS |
| F-04 | Registrasi akun baru | Nama, email baru, password ≥ 6 karakter | Akun dibuat, langsung masuk ke toko | Akun terdaftar dan redirect ke toko | ✅ PASS |
| F-05 | Registrasi dengan email yang sudah ada | Email yang sudah dipakai akun lain | Muncul pesan "Email sudah terdaftar!" | Toast error muncul | ✅ PASS |
| F-06 | Tambah produk baru (Admin) | Isi semua field wajib produk | Produk tersimpan dan muncul di daftar | Produk berhasil ditambahkan | ✅ PASS |
| F-07 | Edit produk (Admin) | Ubah nama/harga produk | Data produk terupdate | Perubahan tersimpan dan tampil | ✅ PASS |
| F-08 | Hapus produk (Admin) | Klik hapus pada produk | Produk terhapus dari daftar | Produk berhasil dihapus | ✅ PASS |
| F-09 | Tambah produk ke keranjang (User) | Klik tombol + pada produk | Item masuk ke keranjang, counter bertambah | Keranjang terupdate | ✅ PASS |
| F-10 | Update quantity di keranjang | Klik + atau - pada item keranjang | Qty berubah, total harga terupdate | Perhitungan total akurat | ✅ PASS |
| F-11 | Hapus item dari keranjang | Klik tombol ✕ pada item | Item hilang dari keranjang | Item berhasil dihapus | ✅ PASS |
| F-12 | Proses checkout | Isi alamat & pilih metode bayar | Pesanan terbuat, keranjang kosong | Order ID baru terbuat | ✅ PASS |
| F-13 | Lihat daftar pesanan (User) | Buka halaman Pesanan | Menampilkan pesanan milik user yang login | Hanya pesanan user sendiri yang tampil | ✅ PASS |
| F-14 | Filter pesanan berdasarkan status | Klik tab filter status | Menampilkan pesanan sesuai status filter | Filter berfungsi | ✅ PASS |
| F-15 | Update status pesanan (Admin) | Pilih status baru pada dropdown | Status pesanan berubah | Status terupdate di database | ✅ PASS |
| F-16 | Pencarian produk | Ketik kata kunci di search bar | Menampilkan produk yang sesuai | Filter pencarian berfungsi | ✅ PASS |
| F-17 | Filter produk berdasarkan kategori | Klik tombol kategori | Produk difilter sesuai kategori | Hanya produk kategori terpilih yang tampil | ✅ PASS |
| F-19 | Register dengan format email salah | Email: `kurnia` | Peringatan format email muncul, akun tidak dibuat | Peringatan tampil | ✅ PASS |
| F-20 | Lupa password dengan email terdaftar | Email akun valid | Kode reset 6 digit ditampilkan, form reset terbuka | Berhasil | ✅ PASS |
| F-21 | Lupa password dengan email tidak terdaftar | Email belum terdaftar | Peringatan "Email belum terdaftar" | Peringatan tampil | ✅ PASS |
| F-22 | Reset password dengan kode benar | Kode benar + password baru ≥ 6 + konfirmasi sama | Password berubah, kembali ke login; password lama tidak bisa dipakai | Berhasil | ✅ PASS |
| F-23 | Reset password dengan kode salah / konfirmasi beda / password pendek | Input tidak valid | Peringatan di field terkait, password tidak berubah | Peringatan tampil | ✅ PASS |
| F-18 | Logout | Klik tombol Keluar | Kembali ke halaman login | Redirect ke auth screen | ✅ PASS |

### 2. Pengujian Keamanan (Security Testing)

| No | Skenario Uji | Input | Output yang Diharapkan | Hasil | Status |
|----|-------------|-------|----------------------|-------|--------|
| S-01 | Akses fitur admin tanpa login | Buka app tanpa login | Tetap di halaman login | Halaman login ditampilkan | ✅ PASS |
| S-02 | User biasa tidak bisa akses menu admin | Login sebagai user | Menu admin tidak muncul di navbar | Navbar hanya tampil menu user | ✅ PASS |
| S-03 | Admin tidak bisa tambah ke keranjang | Login sebagai admin | Tombol keranjang disembunyikan | Tombol cart tidak tampil untuk admin | ✅ PASS |
| S-04 | Registrasi dengan password pendek | Password: "abc" | Muncul error validasi | Toast "Password min 6 karakter!" | ✅ PASS |
| S-06 | Menyalin isi field password | Ctrl+C / Ctrl+X / klik kanan salin | Aksi diblokir, muncul toast | Terblokir | ✅ PASS |
| S-07 | Login dengan akun user demo lama | `user@bizmart.id` / `user123` | Ditolak | Email atau password salah | ✅ PASS |
| S-05 | User hanya lihat pesanannya sendiri | Login sebagai user | Hanya pesanan userId sendiri tampil | Data pesanan terfilter per user | ✅ PASS |

### 3. Pengujian Kegunaan (Usability Testing)

| No | Aspek | Skenario | Hasil Observasi | Penilaian |
|----|-------|----------|----------------|-----------|
| U-01 | Kemudahan Login | Pengguna baru mencoba login | Tombol "Isi ↗" membantu mengisi demo akun dengan cepat | ✅ Mudah |
| U-02 | Navigasi Menu | Berpindah antar halaman | Navbar jelas, aktif state terlihat dengan warna berbeda | ✅ Intuitif |
| U-03 | Proses Belanja | Menambah produk ke cart & checkout | Flow: lihat produk → cart → checkout dalam 3 langkah | ✅ Efisien |
| U-04 | Feedback Aksi | Setiap aksi penting | Toast notification muncul untuk setiap aksi | ✅ Informatif |
| U-05 | Mobile Experience | Buka di layar ≤ 768px | Hamburger menu, grid responsif, sidebar full-width | ✅ Responsif |
| U-06 | Pelacakan Pesanan | Lihat status pesanan | Tracker visual step-by-step memudahkan monitoring | ✅ Jelas |
| U-07 | Pengelolaan Admin | Operasi CRUD produk | Form modal yang jelas dengan validasi | ✅ Terstruktur |

### 4. Pengujian Kinerja (Performance Testing)

| No | Skenario | Kondisi | Hasil | Status |
|----|----------|---------|-------|--------|
| P-01 | Load awal halaman | Buka index.html | Tampil < 2 detik (single file, no external backend) | ✅ PASS |
| P-02 | Filter produk | 10+ produk difilter | Respons instan (< 100ms, client-side) | ✅ PASS |
| P-03 | Update keranjang | Tambah/hapus item | Perubahan real-time tanpa delay | ✅ PASS |
| P-04 | Persistensi data | Refresh halaman setelah simpan data | Data produk & pesanan tetap tersimpan via localStorage | ✅ PASS |
| P-05 | Responsivitas animasi | Animasi transisi halaman | Smooth 0.3s, tidak lag | ✅ PASS |

### 5. Pengujian Kompatibilitas (Compatibility Testing)

| No | Platform | Browser | Hasil |
|----|----------|---------|-------|
| C-01 | Desktop | Google Chrome 124+ | ✅ Berfungsi Normal |
| C-02 | Desktop | Mozilla Firefox 125+ | ✅ Berfungsi Normal |
| C-03 | Desktop | Microsoft Edge 124+ | ✅ Berfungsi Normal |
| C-04 | Mobile | Chrome Android | ✅ Responsif & Berfungsi |
| C-05 | Mobile | Safari iOS | ✅ Responsif & Berfungsi |
| C-06 | Tablet | Chrome iPad | ✅ Layout Menyesuaikan |

---

## 🛠️ Teknologi yang Digunakan

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Penyimpanan Data:** localStorage (client-side persistence)
- **Font:** Plus Jakarta Sans, Space Grotesk (Google Fonts)
- **Deploy:** GitHub Pages / Vercel / Netlify
- **Tidak memerlukan backend server**

---

## 📁 Struktur Proyek

```
bizmart-umkm/
├── index.html      # Aplikasi lengkap (single-file)
└── README.md       # Dokumentasi & pengujian
```

---

## 🚀 Cara Menjalankan

1. **Clone atau download** file `index.html`
2. **Buka di browser** — tidak perlu server!
   ```
   Klik 2x file index.html
   atau
   Buka dengan Live Server di VS Code
   ```
3. **Login** atau **daftar akun baru** melalui halaman autentikasi

---

## 📸 Fitur Utama per Role

### 👤 User
- Lihat & cari produk UMKM
- Filter produk berdasarkan kategori
- Tambahkan produk ke keranjang belanja
- Checkout dengan pilihan metode pembayaran
- Lacak status pesanan secara real-time

### 🛡️ Admin
- Dashboard statistik pendapatan, pesanan, produk, user
- CRUD produk (Create, Read, Update, Delete)
- Kelola & update status semua pesanan
- Manajemen pengguna terdaftar

---

## 👩‍💻 Pengembang

**Kurnia Nurhajijah**  
NIM: 202310370311260  
Rekayasa Kebutuhan D  
Universitas Muhammadiyah Malang
