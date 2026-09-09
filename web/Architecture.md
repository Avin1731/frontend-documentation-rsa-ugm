# Architecture - Web Dashboard

## Topologi Repositori
Untuk menghindari konflik lintas disiplin, Web Dashboard memiliki repositori terpisah dari Core Backend (WP-3) dan Mobile Apps. Repositori Web Dashboard sekaligus menampung logika untuk **Next.js BFF**.

## Konsep Arsitektur Layout
Mengadopsi pola arsitektur dari *project* sebelumnya (Evolusi PL), aplikasi Web akan menggunakan sistem layout yang modular:
- **DashboardLayout Component**: Sebuah komponen *wrapper* (analoginya seperti `PublicLayout`) yang akan secara konsisten membungkus *Header*, *Sidebar* navigasi, dan area konten utama. Ini memastikan elemen-elemen global tidak perlu dimuat ulang pada setiap perpindahan halaman.

## Modularisasi Rute & API (BFF)
- **Struktur Rute Terpisah**: Sama halnya dengan pemisahan `routes/public.php` dan `routes/admin.php`, *endpoint* pada Next.js API Routes akan dipecah secara rapi ke dalam modul-modul spesifik, seperti:
  - `/api/auth/` (Login & validasi token)
  - `/api/tanks/` (Data master tangki)
  - `/api/alerts/` (Riwayat peringatan/log)
  Hal ini krusial agar 2 developer yang fokus di Web dapat bekerja secara paralel tanpa mengalami bentrok kode (*merge conflict*).

## Git Branching Strategy
- Menerapkan alur berjenjang: `main` (produksi/stabil) -> `dev` (integrasi) -> `feature/*` (pengembangan fitur spesifik).
- Dilengkapi dengan *Branch Protection Rules* pada cabang `main` dan `dev` sehingga integrasi kode wajib melalui mekanisme *Pull Request* dan tinjauan kode.
