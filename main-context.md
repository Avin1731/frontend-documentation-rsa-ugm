# SISTEM INFORMASI PEMANTAUAN DAN PENGENDALIAN LEVEL AIR BERBASIS IOT DI RSA UGM
**Nama Dokumen**: WP4-Multi-Platform Dashboard (Web & Android) & AAA
**Deskripsi**: Master Context Document untuk pengembangan antarmuka (Frontend) Web dan Mobile App.

## 1. Arsitektur dan Infrastruktur Frontend
Bagian ini mendefinisikan landasan teknis untuk proyek WP-4, mencakup Web dan Mobile.

### Spesifikasi Tech Stack
- **Web Dashboard**: Next.js & Tailwind CSS.
- **Mobile App**: React Native (atau Expo).
- **Backend-for-Frontend (BFF)**: Next.js API Routes berfungsi sebagai BFF. 

### Mekanisme Backend-for-Frontend (BFF)
Mengapa Next.js BFF Adalah Titik Ideal (Sweet Spot):
1. **Infrastruktur Efisien**: Fungsi peladen perantara berjalan bersamaan dengan dashboard web tanpa perlu setup server, port, atau deployment terpisah.
2. **Sentralisasi Logika**: BFF menerima data mentah dari backend inti (WP-3), melakukan kalkulasi/pemrosesan (seperti mapping nama variabel `tank_lvl` menjadi `waterVolume`), dan mendistribusikan JSON bersih ke klien Web dan Mobile. Jika ada perubahan dari backend, cukup ubah di satu tempat.
3. **Keamanan Sesi**: Menggunakan HTTP-only cookies di sisi server Next.js untuk mengamankan token autentikasi (AAA) agar tidak terekspos langsung ke aplikasi klien, mencegah pencurian sesi.

### Topologi Repositori
Pemisahan tegas menjadi 3 bagian:
- **Repo Web Dashboard** (Termasuk BFF)
- **Repo Mobile Apps**
- **Repo Core Backend** (WP-3)

## 2. Integrasi Data dan Kesepakatan API (API Contract)
Komunikasi data antara WP-3 (Backend) dan WP-4 (Frontend via BFF).

### Kebutuhan Data Mentah (Dari WP-3)
Berdasarkan *requirements* dari WP-3:
- **REST API**: Mengambil data historis/log (grafik 24 jam), data master tangki (`tanks`), dan riwayat log.
- **WebSocket**: Channel realtime untuk pembaruan level air persentase secara instan dan push notifikasi untuk peringatan/alerts.
- **Data Status**: WARNING (30-60%) dan CRITICAL (<30%). Konfirmasi aktuasi pompa (opsional, karena status aktuator masih TBD di WP-3).

### Struktur Respon BFF (Ke Klien)
- BFF menyajikan JSON yang bersih dan seragam. Komponen UI Web dan Mobile hanya melakukan proses rendering tanpa perlu kalkulasi logika tambahan.

### Sistem Keamanan & Autentikasi (AAA)
- Alur Role-Based Access Control (RBAC) untuk admin/operator.
- Pembuatan token akses di WP-3, disimpan secara aman menggunakan mekanisme BFF Next.js (HTTP-only cookies).
- Pencatatan Audit Log untuk setiap akses (login, kontrol manual - jika ada).

## 3. Panduan Antarmuka dan Alur Kerja Tim
Acuan visual dan operasional untuk 4 anggota tim WP-4.

### Design System & Komponen Visual
- **Standarisasi Warna**: Penekanan pada status level air (misal, merah untuk CRITICAL <30%, kuning untuk WARNING 30-60%).
- **Layout Fleksibel**: 
  - *Web*: Dioptimalkan untuk layar monitor ultrawide di rumah sakit.
  - *Mobile*: Dioptimalkan untuk layar vertikal pada ponsel pintar operator.

### Manajemen State & Pustaka Grafik
- **State Management**: Menyimpan status data tangki realtime.
- **Library Grafik**: Visualisasi grafik historis 24 jam untuk Web dan Mobile.

### Pembagian Tugas
- **Tim Web (2 Orang)**: Fokus pada Next.js Dashboard dan API Routes (BFF).
- **Tim Mobile (2 Orang)**: Fokus pada aplikasi React Native Android.
*(Detail Work Breakdown Structure (WBS) akan dijabarkan lebih lanjut).*

## 4. Referensi Arsitektur & Alur Kerja (Adaptasi Project Evolusi PL)
Mengadopsi pola arsitektur dari *project* Evolusi PL sebelumnya untuk efisiensi kolaborasi:
- **Modularisasi Rute & API**: Pemisahan secara terstruktur. Pada Next.js BFF, endpoint API akan dipecah menjadi modul spesifik (misal: `/api/auth`, `/api/tanks`, `/api/alerts`) menyerupai pemisahan `routes/public.php` dan `routes/admin.php` untuk menghindari konflik *merge* antar anggota tim.
- **Git Branching Strategy**: Menerapkan alur `main` (stabil) -> `dev` (integrasi) -> `feature/*`. Dilengkapi dengan *Branch Protection* di `main` dan `dev` (wajib Pull Request).
- **Otomasi CI/CD (GitHub Actions)**: Pipeline otomatis dengan *Job Paralel* untuk *Linting* (ESLint/Prettier) dan *Testing* (Jest) yang wajib **HIJAU** sebelum proses *merge* Pull Request.
