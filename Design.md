# Design Specification: SUWARNO (Aplikasi Akuntansi Kontrakan)

## 1. Visi Desain & Arahan Utama (Core Directive)
Aplikasi **SUWARNO** tidak boleh terlihat seperti aplikasi akuntansi konvensional atau *template* PWA standar. UI/UX harus dirancang dengan pendekatan *high-end agency*, memberikan kesan premium, eksklusif (*tasteful*), dan memiliki interaksi yang sangat mulus (fluid) layaknya aplikasi berstandar kelas dunia. 

- **Fokus Utama**: Kedalaman fisik visual (haptic depth), ritme spasial yang dinamis, obsesi pada micro-interactions, dan pergerakan/animasi yang *fluid*.
- **Anti-Pattern yang Dilarang**: Menggunakan font generik (Inter, Roboto, Arial, dll), icon set dengan garis tebal standar, shadow gelap bawaan (`shadow-md`), garis batas 1px solid abu-abu yang membosankan, dan susunan *grid* simetris statis tanpa ruang kosong yang lega.

## 2. Tema & Tekstur (Vibe & Texture Archetype)
Berdasarkan konteks aplikasi pencatatan keuangan modern untuk *shared space* (kontrakan), **SUWARNO** akan mengadopsi perpaduan **Soft Structuralism** dengan sentuhan **Ethereal Glass**:
- **Background & Lapisan**: Latar belakang akan didominasi oleh warna sangat bersih (seperti Silver-grey sangat terang atau Pure White) di *light mode*, dipadukan dengan efek kaca buram dalam (Deep Glassmorphism / `backdrop-blur-2xl`) pada elemen *floating*.
- **Tipografi Utama**: Wajib menggunakan font *premium modern Grotesk* (seperti `Geist`, `Plus Jakarta Sans`, atau `Clash Display`). Ukuran teks heading (*H1/H2*) dibuat masif, tebal, dan berani untuk memberikan hierarki visual yang jelas.
- **Ambient Shadows**: Menggunakan shadow yang tersebar (*highly diffused*) dan sangat lembut. Menggantikan *drop shadow* pekat agar elemen UI tampak "ringan", mengambang, dan futuristik.

## 3. Komponen & Struktur Estetika (Haptic Micro-Aesthetics)

### A. Arsitektur "Double-Bezel" (Doppelrand)
Kartu data transaksi, baris *leaderboard*, atau kotak laporan keuangan di SUWARNO tidak boleh sekadar diletakkan rata. Mereka harus dirancang seperti perpaduan perangkat keras (hardware) mewah:
- **Outer Shell**: Pembungkus luar memiliki *background* yang nyaris transparan (`bg-black/5` atau `bg-white/5`), batas tipis (*hairline border*), bantalan/padding spesifik, dan radius kelengkungan yang ekstrim besar (`rounded-[2rem]`).
- **Inner Core**: Kontainer utama (berisi nilai transaksi / keterangan) diletakkan di dalamnya, memiliki warna latar spesifik, dan garis batas/pantulan sinar *inset* tipis (seolah ada pelat kaca). Radius kelengkungan dalam dikalkulasi secara presisi (`rounded-[calc(2rem-0.375rem)]`) agar konsentris sempurna.

### B. Arsitektur Tombol CTA ("Island" Button)
- **Bentuk Pil Utuh**: Tombol *Primary* ("Catat Pengeluaran", "Kirim Pembayaran", dll) wajib berbentuk pil bundar seutuhnya (`rounded-full`) dengan ruang kosong (padding) yang berlimpah (seperti `px-6 py-3`).
- **Pola "Button-in-Button"**: Ikon petunjuk (seperti panah) di dalam tombol TIDAK boleh menempel langsung di sebelah teks. Ikon tersebut wajib dimasukkan kembali ke dalam pelindung lingkaran kecil miliknya sendiri yang warnanya sedikit dibedakan, diposisikan rata di ujung paling kanan batas tombol.

### C. Spasial & Ritme Ruang (Whitespace)
- **Macro-Whitespace**: Jangan hemat spasi. Gunakan penggandaan dari *padding* standar. Jarak antar seksi halaman (misal antara Dashboard dan Riwayat Transaksi) menggunakan jarak vertikal masif (contoh: `py-24` sampai `py-40`). 
- **Eyebrow Tags**: Tiap judul H1/H2 (contoh: pada judul halaman Leaderboard) didahului dengan *badge/tag* berukuran mikroskopis berbentuk pil, teks huruf besar (uppercase), dan jarak antar huruf dilebarkan ekstrim (`tracking-[0.2em]`).

## 4. Koreografi Animasi & Pergerakan (Motion Choreography)

Sistem SUWARNO menolak penggunaan animasi linier standar (`ease-in-out` bawaan). Segala bentuk pergerakan harus menyimulasikan fisika pegas benda padat di dunia nyata menggunakan kalkulasi *custom cubic-bezier* (contoh: `ease-[cubic-bezier(0.32,0.72,0,1)]`).

- **Fisika Tombol Hover Magnetik**: Saat area transaksi, menu, atau tombol di-hover, perubahan tidak boleh hanya sekadar warna latar. Seluruh struktur harus sedikit mengecil layaknya ditahan oleh tekanan fisik (`active:scale-[0.98]`). Ikon *button-in-button* di dalamnya ikut bergeser secara diagonal seakan menahan tegangan mekanik internal.
- **Interpolasi Gulir (Scroll Entry)**: Data transaksi, laporan, atau menu tidak boleh tampil mendadak dan kaku. Saat halaman digulir dan mereka masuk dalam pandangan (viewport), elemen-elemen tersebut harus naik dan memudar masuk secara elegan (`translate-y-16 blur-md opacity-0` berevolusi perlahan ke posisi aslinya `translate-y-0 blur-0 opacity-100` selama >800ms).
- **Navigasi "Fluid Island"**: *Bottom Navigation Bar* untuk mobile (atau menu desktop) muncul sebagai "pil kaca mengambang" di tepi layar. Jika ada menu diperluas, panel tersebut memenuhi layar menggunakan blur sangat pekat (`backdrop-blur-3xl`) dengan *item* menunya bermunculan bertahap dari bawah ke atas menggunakan penundaan berjenjang (*staggered mask reveal*).

## 5. Perlindungan Performa & Optimalisasi

- **GPU-Safe Animation**: Semua animasi UI pada SUWARNO (masuk, klik, muat) dilarang menggunakan animasi pergeseran properti geometri asli (`top`, `left`, `width`, `height`) karena memberatkan HP. Semua gerak secara eksklusif digerakkan oleh `transform` dan `opacity`.
- **Aturan Pembatasan Blur**: Efek kaca (*backdrop-blur*) adalah komponen terberat untuk baterai. Efek blur ini HANYA dibolehkan menempel pada panel *fixed/sticky* (navbar, overlay modal, pop-up konfirmasi bukti transfer). Jangan pernah pasangkan pada lapisan latar dari elemen *scrolling list* riwayat pengeluaran.
- **Runtuhan Mobile yang Mulus (Mobile Collapse)**: Segala susunan desain yang kompleks, saling tumpang tindih (*z-axis cascade*), atau grid asimetris di tampilan desktop diwajibkan untuk diubah *(collapse)* secara penuh dan bersih menjadi tumpukan satu lajur vertikal (`grid-cols-1`, `w-full`, dengan *gap* lega) saat diakses melalui *smartphone* (viewport di bawah 768px). Area sentuh untuk mengunggah bukti pembayaran harus bebas konflik sentuh jempol.

---
**Tujuan Akhir (Final Polish Check):** 
Desain aplikasi SUWARNO akan menyampaikan nilai lebih dari sekadar "Aplikasi Catatan Kontrakan Mahasiswa/Karyawan". Tampilannya akan merepresentasikan pengalaman visual kelas eksekutif yang sering dijumpai pada *fintech startup* bernilai tinggi.
