# Spesifikasi High-Level & Alur Sistem: Aplikasi Akuntansi Kontrakan "Suwarno"

## 1. Latar Belakang & Tujuan (Background & Objective)
Kontrakan yang dihuni oleh 4 orang membutuhkan sebuah sistem pencatatan keuangan bersama yang transparan, mudah diakses, dan cepat (tidak lambat/ngelag). Tujuan utama aplikasi ini adalah untuk melacak uang kas bersama, mencatat pengeluaran rutin bulanan (seperti listrik, air, iuran sampah), pengeluaran operasional tak terduga, pembayaran Iuran Sewa Kontrakan, donasi Guest, serta pemasukan kas lainnya.

Aplikasi ini ditargetkan berupa PWA (Progressive Web App) dengan pendekatan *mobile-first* agar penghuni dapat dengan cepat memasukkan data transaksi melalui *smartphone* mereka kapan saja. Aplikasi juga harus memfasilitasi konfirmasi pembayaran secara manual (upload bukti pembayaran) tanpa menggunakan payment gateway.

## 2. Kebutuhan Pengguna (User Needs & Personas)

Terdapat dua kelompok pengguna utama:

**A. Admin (4 Penghuni Kontrakan)**
*   Kebutuhan: 
    *   Ingin mencatat pengeluaran (baik rutin maupun mendadak) dengan cepat tanpa form yang rumit.
    *   Ingin mencatat pemasukan (misal: patungan bulanan, uang Iuran Sewa Kontrakan).
    *   Ingin melihat sisa saldo kas kontrakan secara *real-time*.
    *   Ingin melihat riwayat transaksi agar transparan (siapa yang mencatat, untuk apa, kapan).
    *   Ingin melihat pengeluaran terbanyak (leaderboard pengeluaran) dan siapa yang menyumbang Kas terbanyak.
    *   Mampu melakukan pembayaran dan mengunggah bukti pembayaran (struk/screenshot transfer).

**B. Guest (Tamu / Pihak Luar)**
*   Kebutuhan:
    *   Hanya perlu melihat laporan transparansi dana (saldo, total pemasukan, total pengeluaran).
    *   Ingin dapat memberikan "Donasi Guest" ke kas kontrakan dengan cara transfer dan upload bukti pembayaran.
    *   Tidak boleh memiliki akses untuk mengubah, menambah, atau menghapus data keuangan apa pun (selain melakukan input donasi guest).

## 3. Spesifikasi Kebutuhan Sistem (High-Level Features)

1.  **Sistem Akun Berbasis Peran (Role-based Access)**
    *   Aplikasi hanya mengizinkan 4 akun khusus sebagai Admin.
    *   Aplikasi memiliki 1 akun Guest (read-only pada data, bisa melakukan Donasi).
2.  **Dashboard Ringkasan Cepat (Quick Glance Dashboard)**
    *   Langsung menyajikan informasi krusial saat aplikasi dibuka: Saldo Kas, Total Pengeluaran Bulan Ini, Total Pemasukan Bulan Ini.
3.  **Manajemen Transaksi (Inti Aplikasi)**
    *   Pencatatan Pemasukan (Income) termasuk Iuran Sewa Kontrakan, Donasi Guest.
    *   Pencatatan Pengeluaran (Expense).
    *   Kategorisasi transaksi (Pengeluaran Rutin vs Operasional).
4.  **Sistem Pembayaran Manual & Bukti Transfer**
    *   Sistem pembayaran konvensional (transfer manual).
    *   Pengguna (Admin/Guest) wajib mengunggah bukti pembayaran (foto struk/screenshot) saat membayar sewa, patungan, atau donasi.
5.  **Sistem Leaderboard & Sorting**
    *   **Sorting Pengeluaran Terbanyak**: Menampilkan daftar pengeluaran yang diurutkan dari nominal terbesar ke terkecil.
    *   **Leaderboard Kas Terbanyak**: Menampilkan peringkat penghuni (Admin) berdasarkan kontribusi patungan/kas terbanyak.
6.  **Pelaporan & Transparansi (Reporting)**
    *   Menyajikan laporan bulanan sederhana berupa grafik visual yang mudah dipahami (tidak terlihat seperti tabel Excel yang kaku).
7.  **Aksesibilitas & Performa (PWA & Speed)**
    *   Dapat diinstal di layar utama (Homescreen) *smartphone* seperti aplikasi *native*.
    *   Memuat dengan sangat cepat, mendukung *offline-caching* dasar.
8.  **Desain Visual (UI/UX)**
    *   Tema yang modern, bersih, minimalis, dan *tasteful* (estetik). Tidak kaku dan tidak generik.

## 4. Alur Sistem Utama (User Flows)

### Alur 1: Pencatatan Pengeluaran Rutin (Flow Admin)
*Kasus: Salah satu penghuni baru saja membayar token listrik.*
1.  **Buka Aplikasi:** Penghuni membuka aplikasi dari homescreen HP. Aplikasi memuat instan (PWA).
2.  **Dashboard:** Penghuni melihat saldo saat ini di dashboard.
3.  **Input:** Penghuni menekan tombol "Tambah Transaksi" (Tombol Floating Action utama yang mencolok).
4.  **Form Cepat:**
    *   Pilih tab "Pengeluaran".
    *   Pilih kategori "Listrik" (berada di urutan teratas karena sering dipakai).
    *   Masukkan nominal (misal: 100.000).
    *   (Opsional) Tambahkan catatan "Listrik bulan September".
5.  **Simpan:** Tekan "Simpan". 
6.  **Selesai:** Aplikasi memberikan notifikasi sukses (Toast). Saldo di dashboard langsung berkurang, dan riwayat transaksi langsung muncul.

### Alur 2: Pembayaran Kas / Iuran Sewa Kontrakan dengan Bukti Transfer (Flow Admin)
*Kasus: Salah satu penghuni menyetor uang sewa bulanan atau uang kas.*
1.  **Transfer Manual:** Penghuni mentransfer dana ke rekening kontrakan.
2.  **Catat Pemasukan:** Penghuni membuka menu "Tambah Pemasukan".
3.  **Input & Upload:** Memilih kategori "Iuran Sewa Kontrakan" atau "Kas", memasukkan nominal, dan *mengunggah screenshot bukti transfer*.
4.  **Simpan & Tampil di Riwayat:** Bukti transfer tersimpan dan dapat dilihat oleh penghuni lain agar transparan.

### Alur 3: Donasi Guest (Flow Guest)
*Kasus: Tamu ingin menyumbang dana ke kontrakan.*
1.  **Akses Guest:** Guest membuka aplikasi dan melihat informasi donasi/rekening kontrakan.
2.  **Input Donasi:** Guest mentransfer dana, lalu menekan tombol "Donasi", memasukkan nama, nominal, dan upload bukti transfer.
3.  **Simpan:** Donasi masuk ke sistem sebagai pemasukan tertunda hingga diverifikasi Admin (atau langsung tercatat).

### Alur 4: Pengecekan Laporan Bulanan & Leaderboard (Flow Admin & Guest)
*Kasus: Akhir bulan, penghuni ingin tahu kemana saja uang kas dihabiskan dan siapa penyumbang terbanyak.*
1.  **Buka Menu Laporan:** Pengguna masuk ke menu "Laporan" atau "Statistik".
2.  **Lihat Grafik:** Sistem menampilkan grafik lingkaran/batang porsi pengeluaran bulan ini.
3.  **Lihat Leaderboard:** Pengguna melihat *Sorting Pengeluaran Terbanyak* (untuk evaluasi penghematan) dan *Leaderboard Kas Terbanyak* (ranking penyumbang kas/iuran tertinggi).
4.  **Evaluasi:** Pengguna dapat melihat total pengeluaran dan memastikan apakah masih sesuai *budget* patungan.

## 5. Kriteria Sukses (Success Criteria)
1.  Aplikasi berhasil digunakan oleh ke-4 penghuni tanpa kebingungan (UX yang intuitif).
2.  Waktu yang dibutuhkan untuk mencatat satu transaksi baru tidak lebih dari 10 detik.
3.  Fungsi upload bukti transfer berfungsi dengan lancar tanpa error pada perangkat *mobile*.
4.  Tidak ada kendala *lagging* atau lambat (Page Load Time < 2 detik).
5.  Data saldo, pengeluaran terbesar, dan leaderboard penyumbang selalu akurat dan tersinkronisasi antar ke-4 Admin.
6.  Guest tidak dapat memanipulasi data melalui cara apa pun (hanya bisa menambah donasi dan upload buktinya).
