# 🏡 SUWARNO — Aplikasi Akuntansi Kontrakan

Selamat datang di repositori **SUWARNO**, sebuah sistem pencatatan keuangan bersama (*Progressive Web App*) yang dirancang khusus untuk mempermudah transparansi dan pengelolaan uang kas, iuran sewa, serta pengeluaran rutin penghuni kontrakan.

Aplikasi ini tidak dirancang dengan pendekatan konvensional, melainkan menerapkan standar visual *High-End Agency* yang premium, ringan, dan sangat intuitif (lihat detail desain pada file `Design.md`).

---

## 📑 Spesifikasi & Dokumentasi Proyek

Sebelum mulai berkontribusi atau melakukan eksekusi (*coding*), **wajib** membaca dan memahami dua dokumen utama berikut:

1. **[issue.md](./issue.md)**
   Berisi Spesifikasi Sistem secara menyeluruh, termasuk:
   - Alur Pengguna (*User Flow*) untuk Admin (Penghuni) dan Guest.
   - Manajemen Transaksi (Iuran Sewa, Donasi Guest, Kas, Pengeluaran Rutin).
   - Fitur Pembayaran Manual dengan wajib upload Bukti Transfer (tanpa *Payment Gateway*).
   - Sistem *Leaderboard* Kontribusi dan *Sorting* Pengeluaran Terbesar.
   - Target Performa dan Kriteria Sukses.

2. **[Design.md](./Design.md)**
   Berisi Pedoman Mutlak Visual & UI/UX, mencakup:
   - Penggunaan arsitektur *Double-Bezel (Doppelrand)*.
   - Interpolasi gulir (*Scroll Entry*) dan Koreografi Gerakan (*Motion Choreography*) menggunakan fisika kubik.
   - Larangan keras terhadap struktur generik (anti-patterns) untuk mempertahankan nuansa aplikasi bernilai tinggi (Ethereal Glass & Soft Structuralism).

---

## 🚀 Fitur Utama
*   **Role-Based Access**: 4 akun khusus Penghuni (Admin) dan 1 akun Tamu (Guest).
*   **Pencatatan Keuangan Transparan**: Catat pengeluaran listrik, sampah, galon, dsb secara instan.
*   **Pembayaran Kas/Sewa**: Transfer manual dan lampirkan bukti pembayaran untuk saling divalidasi antar penghuni.
*   **Leaderboard**: Lihat siapa penyumbang/kas terbanyak dan lacak pengeluaran terbesar.
*   **Donasi Eksternal**: Tamu/pihak luar dapat menyumbang secara sukarela melalui akses *Guest*.
*   **Progressive Web App (PWA)**: Bisa diinstal di layar utama *smartphone* (iOS & Android) layaknya aplikasi *native*, sangat responsif dan ringan.

---

## ⚙️ Rencana Teknologi (*Tech Stack*)
*(Dapat disesuaikan oleh Agent Eksekutor berdasarkan `issue.md`)*
*   **Frontend**: Vite + Svelte / Vanilla JS ES Modules (berfokus pada *mobile-first* dan kecepatan ekstrem).
*   **Styling**: Vanilla CSS Variables / Tailwind (disesuaikan dengan parameter di `Design.md`).
*   **Backend & DB**: Node.js/Express (SQLite) atau Supabase/Firebase (PostgreSQL/NoSQL).
*   **Deploy/PWA**: vite-plugin-pwa (Service Workers).

---

*(Dokumen ini merupakan representasi tingkat tinggi dari proyek. Selalu rujuk ke `issue.md` untuk implementasi teknis lebih rinci).*
