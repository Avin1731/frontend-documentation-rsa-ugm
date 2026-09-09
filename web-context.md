# SISTEM INFORMASI PEMANTAUAN DAN PENGENDALIAN LEVEL AIR BERBASIS IOT DI RSA UGM
**Nama Dokumen**: WP4 - Context Khusus Web Dashboard & BFF
**Fokus**: Pengembangan Web Dashboard Ultrawide & Next.js API Routes (BFF)

## 1. Arsitektur dan Infrastruktur Web & BFF
### Spesifikasi Tech Stack
- **Framework Utama**: Next.js.
- **Styling**: Tailwind CSS v4.
- **BFF (Backend-for-Frontend)**: Menggunakan fitur Next.js API Routes (Serverless Functions / Node.js runtime).

### Mekanisme Next.js BFF Adalah Titik Ideal
1. **Infrastruktur Efisien**: API BFF dan Frontend Web disajikan dari satu deployment (Next.js). Tidak perlu *container* terpisah untuk middleware.
2. **Sentralisasi Logika**: API Routes di Next.js bertugas mengambil data dari Core Backend (WP-3), membersihkan struktur JSON-nya (misalnya mengubah field raw seperti `tank_lvl` menjadi `waterVolume`), dan menyediakan endpoint tunggal yang rapi untuk dikonsumsi Frontend Web maupun Mobile.
3. **Keamanan Sesi**: BFF mengamankan kredensial AAA (Autentikasi, Autorisasi, Akunting) dari WP-3. JWT token dari WP-3 akan disimpan di dalam `HTTP-Only Cookies` di Next.js sehingga Frontend Web tidak pernah memiliki akses langsung ke token mentah tersebut (menghindari serangan XSS).

## 2. Integrasi Data dan API Contract (Sisi Web)
### Struktur Respon BFF (Ke Klien Web)
BFF akan mengembalikan JSON yang sudah diproses dan diformat agar langsung di-looping atau dirender oleh komponen React di Next.js.

### Kebutuhan Data Mentah (Dari WP-3 -> BFF -> Web)
- **REST API (Histori & Auth)**: Mengakses histori data log 24 jam untuk chart dan melakukan proses verifikasi login.
- **WebSocket (Realtime)**: BFF (atau Web client) mendengarkan stream WebSocket dari WP-3 untuk memutakhirkan dashboard secara instan (mengurangi latensi).

### Sistem Keamanan & Autentikasi (AAA)
- Web akan menggunakan form login standar yang menembak API Routes Next.js.
- API Routes (Next.js) meneruskan kredensial ke WP-3, mengambil token JWT, dan mengatur header `Set-Cookie` secara aman.

## 3. Panduan Antarmuka dan Scope Web
### Design System & Komponen Visual
- **Layout Ultrawide**: Web ini dirancang secara khusus untuk diakses dari layar monitor *ultrawide* yang digunakan oleh pengawas di rumah sakit.
- **Indikator Visual**: Menggunakan kelas Tailwind CSS untuk state level air:
  - CRITICAL (< 30%) : Warna dominan Merah.
  - WARNING (30 - 60%) : Warna dominan Kuning/Oranye.
  - NORMAL (> 60%) : Warna dominan Hijau/Biru.

### Adaptasi Arsitektur Project Sebelumnya (Evolusi PL)
- **Modular Layout**: Mengadopsi konsep `PublicLayout`, Web Dashboard Next.js akan memisahkan layout menjadi komponen modular (misal: `DashboardLayout` yang secara rapi membungkus `Sidebar`, `Header`, dan `Content Area`).
- **Interaksi UI yang Terkontrol**: Berkaca dari fitur galeri interaktif (*click-to-lock*), status indikator tangki dan komponen *overlay/modal* grafik histori dirancang tanpa penumpukan *state* animasi ganda, memastikan *user experience* (UX) responsif namun bersih.
- **Pemisahan Logika API Routes**: Struktur endpoint BFF dipecah sedari awal untuk mencegah konflik ketika tim developer web bekerja paralel.

### Scope Halaman Dashboard Web
Berdasarkan *requirements*, halaman minimal yang harus ada:
1. **Halaman Login**: Untuk AAA, menginputkan kredensial.
2. **Dashboard Utama (Monitoring)**: Menampilkan card ringkasan seluruh tangki (Tangki Atap, Rawat Inap, Bedah, dll). Terdapat indikator real-time dan notifikasi *alert*.
3. **Detail Tangki & Grafik**: Halaman khusus yang memuat grafik historis 24 jam dari satu tangki tertentu.
4. **Halaman Audit & Log**: Tabel daftar riwayat peringatan, log aktivitas user, dan riwayat aksi (jika berlaku).
