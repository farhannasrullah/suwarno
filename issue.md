# Spesifikasi Low-Level: Sistem Akuntansi Sederhana Kontrakan "Suwarno"

## 1. Ringkasan Proyek
Membangun aplikasi PWA (Progressive Web App) untuk pencatatan keuangan (pemasukan dan pengeluaran) kontrakan. Sistem akan diakses oleh 4 penghuni (sebagai Admin) dan pihak luar (sebagai Guest). 
Aplikasi harus dioptimalkan untuk performa tinggi (tidak ngelag) dan memiliki UI/UX yang menarik, *tasteful*, dan profesional (tidak terlihat seperti template standar buatan AI).

## 2. Stack Teknologi yang Dipilih
Mempertimbangkan kebutuhan kesederhanaan, performa, dan kemudahan deployment, berikut adalah arsitektur yang ditetapkan:
*   **Frontend**: Svelte (atau SvelteKit) + Vite.
    *   *Alasan*: Svelte sangat ringan karena meng-compile komponen menjadi vanilla JS, tidak ada overhead virtual DOM. Menghasilkan performa yang sangat cepat di perangkat mobile.
*   **Styling**: Tailwind CSS.
    *   *Alasan*: Pengembangan cepat, styling langsung di komponen, sangat mudah dikustomisasi untuk membuat tema yang unik dan *tasteful*.
*   **Backend/Database**: Supabase (PostgreSQL) atau Firebase (Firestore).
    *   *Alasan*: Mengurangi kompleksitas setup server. Menyediakan autentikasi dan database realtime secara *out-of-the-box*. Untuk spesifikasi ini, kita akan asumsikan penggunaan **Supabase**.
*   **PWA**: `vite-plugin-pwa` untuk *service worker*, *caching*, dan *installability*.

## 3. Desain & Tema Visual (Sangat Penting)
*   **Tema Utama**: Clean, modern minimalis. Hindari warna-warna dasar yang mencolok. Gunakan palet warna *earth tone* atau pastel yang kalem dipadu dengan *dark mode* yang elegan.
*   **Tipografi**: Gunakan font modern sans-serif seperti 'Inter', 'Plus Jakarta Sans', atau 'Outfit'.
*   **Interaksi**: Tambahkan micro-interactions yang halus (transisi hover, *active state*, skeleton loading) agar terasa premium. Hindari animasi berlebihan yang mengganggu performa.

## 4. Struktur Database (Supabase / PostgreSQL)

### 4.1 Tabel `users` (dikelola melalui sistem Auth bawaan Supabase)
*   `id` (uuid, PK)
*   `email` (string)
*   `role` (enum: 'admin', 'guest')
*   `display_name` (string)

### 4.2 Tabel `categories`
*   `id` (uuid, PK)
*   `name` (string) - misal: Listrik, Iuran Sampah, Galon, Sewa, dll.
*   `type` (enum: 'income', 'expense')
*   `is_routine` (boolean) - true untuk pengeluaran rutin
*   `icon` (string) - nama icon (misal dari Lucide Icons)

### 4.3 Tabel `transactions`
*   `id` (uuid, PK)
*   `amount` (decimal/integer)
*   `type` (enum: 'income', 'expense')
*   `category_id` (uuid, FK ke categories)
*   `date` (timestamp/date)
*   `description` (text)
*   `created_by` (uuid, FK ke users)
*   `created_at` (timestamp)

## 5. Fitur Utama & Kriteria Penerimaan

### 5.1 Autentikasi & Otorisasi
*   [ ] Sistem login menggunakan email/password.
*   [ ] Terdapat 4 akun Admin (untuk 4 penghuni) yang di-seed saat inisialisasi.
*   [ ] Terdapat 1 akun Guest.
*   [ ] Admin memiliki akses penuh (Create, Read, Update, Delete transaksi & kategori).
*   [ ] Guest HANYA memiliki akses baca (Read-only) pada dashboard dan laporan. Redirect/sembunyikan tombol aksi untuk Guest.

### 5.2 Dashboard Utama
*   [ ] Menampilkan Ringkasan Saldo Saat Ini (Total Pemasukan - Total Pengeluaran bulan ini).
*   [ ] Menampilkan *Card* ringkasan pengeluaran rutin bulan berjalan vs bulan lalu.
*   [ ] Menampilkan *List* transaksi terbaru (5-10 item).

### 5.3 Modul Transaksi (Pemasukan & Pengeluaran)
*   [ ] Form tambah transaksi yang intuitif (menggunakan modal atau halaman terpisah yang cepat diakses).
*   [ ] Input wajib: Nominal, Tipe (Pemasukan/Pengeluaran), Kategori, Tanggal.
*   [ ] Input opsional: Keterangan tambahan.
*   [ ] Validasi form secara *real-time*.

### 5.4 Modul Kategori
*   [ ] Admin dapat menambahkan kategori baru.
*   [ ] Tag khusus untuk mengidentifikasi "Pengeluaran Rutin" (Listrik, Sampah, dll) vs "Pengeluaran Operasional".

### 5.5 Laporan & Analitik Sederhana
*   [ ] Halaman laporan yang menampilkan grafik batang/lingkaran (gunakan library ringan seperti Chart.js atau uPlot) untuk pengeluaran berdasarkan kategori per bulan.
*   [ ] Filter laporan berdasarkan rentang tanggal/bulan.

### 5.6 Konfigurasi PWA
*   [ ] Setup `manifest.json` dengan icon yang sesuai (maskable).
*   [ ] Implementasi *Service Worker* untuk melakukan *cache* pada *static assets* sehingga aplikasi memuat dengan cepat di kunjungan berikutnya.
*   [ ] (Opsional) Mode offline *read-only* jika koneksi terputus.

## 6. Instruksi Eksekusi untuk AI Agent (Tahapan Implementasi)

**FASE 1: Setup & Konfigurasi Awal**
1. Inisialisasi proyek: `npm create vite@latest suwarno-app -- --template svelte-ts` (atau JS sesuai kemampuan).
2. Install dependensi: Tailwind CSS, Supabase JS client, Lucide Svelte (untuk icon), vite-plugin-pwa.
3. Konfigurasi Tailwind (setup theme, colors, fonts) dan Vite PWA.

**FASE 2: Setup Database & Supabase**
1. Buat skema database di Supabase SQL Editor berdasarkan struktur poin 4.
2. Atur Row Level Security (RLS) di Supabase:
   - `transactions` & `categories`: SELECT untuk semua (authenticated), INSERT/UPDATE/DELETE hanya untuk user dengan role 'admin'.
3. Buat file konstan untuk koneksi Supabase (`src/lib/supabase.js`).

**FASE 3: Pengembangan UI Komponen (Komponen Dasar)**
1. Buat komponen Layout utama (Navigation Bar bawah untuk mobile, Sidebar/Header untuk desktop).
2. Buat komponen dasar: Button, Input, Card, Modal. Pastikan styling sesuai panduan "tasteful".

**FASE 4: Pengembangan Fitur (Logic & Integrasi)**
1. Halaman Login.
2. Halaman Dashboard (Fetch data ringkasan).
3. Halaman Daftar Transaksi & Form Tambah Transaksi.
4. Halaman Kategori.
5. Halaman Laporan.

**FASE 5: Poles & Optimasi (Finishing)**
1. Pastikan transisi antar halaman mulus.
2. Audit performa PWA (Lighthouse score target > 90).
3. Periksa tampilan di *viewport* mobile dan desktop.

## Catatan Khusus untuk AI
*   Jangan membuang waktu dengan *boilerplates* berlebihan. Tulis kode yang rapi, *modular*, namun tetap *to-the-point*.
*   Utamakan *User Experience* di mobile karena penghuni kontrakan mayoritas akan menginput transaksi via HP.
*   Gunakan variabel CSS atau Tailwind config untuk warna tema agar mudah diubah nanti.
