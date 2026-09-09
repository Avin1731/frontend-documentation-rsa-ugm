# SISTEM INFORMASI PEMANTAUAN DAN PENGENDALIAN LEVEL AIR BERBASIS IOT DI RSA UGM
**Nama Dokumen**: WP4 - Context Khusus Mobile Apps (Android)
**Fokus**: Pengembangan Aplikasi Mobile (Android) untuk Operator Rumah Sakit

## 1. Arsitektur dan Infrastruktur Mobile
### Spesifikasi Tech Stack
- **Framework Utama**: React Native (atau Expo untuk kemudahan build/delivery ke Android).
- **Styling**: Native StyleSheet atau Tailwind CSS (menggunakan NativeWind).

### Mekanisme Interaksi dengan Next.js BFF
Aplikasi Mobile **TIDAK** langsung menembak endpoint dari Core Backend WP-3. 
1. **Sentralisasi Logika**: Mobile App akan melakukan *fetch* data ke endpoint BFF Next.js. Data yang diterima sudah diformat dengan bersih (tidak ada atribut *raw* yang tidak perlu), menghemat pemrosesan *parsing* di perangkat mobile operator.
2. **Keamanan Sesi**: Proses login pada Mobile Apps menembak endpoint login BFF Next.js. Token kemudian dikelola dengan cara yang aman di perangkat Android (misalnya menggunakan *SecureStore*).

## 2. Integrasi Data dan API Contract (Sisi Mobile)
### Struktur Respon BFF (Ke Klien Mobile)
Mobile App cukup membaca properti JSON spesifik yang disediakan oleh BFF. Format struktur *response* dikunci dan dijamin seragam dengan Web agar logika penampilan datanya identik.

### Kebutuhan Data (BFF -> Mobile)
- **REST API**: Mengambil daftar peringatan (alerts) dan data histori singkat (tidak selengkap Web jika tidak diperlukan, demi hemat *bandwidth* dan kinerja *rendering*).
- **WebSocket / Push Notification**: Aplikasi Mobile membutuhkan *push alert* secara instan jika level air mencapai WARNING (30-60%) atau CRITICAL (<30%). 

### Sistem Keamanan & Autentikasi (AAA)
- Karena Mobile tidak menggunakan *cookies* seperti Web browser, aplikasi akan menerima *Secure Token* dari BFF, kemudian menyimpannya di penampung enkripsi bawaan OS (misalnya *EncryptedSharedPreferences* atau *SecureStore* Expo).

## 3. Panduan Antarmuka dan Scope Mobile
### Design System & Komponen Visual
- **Layout Vertikal (Portrait)**: UI didesain spesifik untuk layar sentuh berorientasi vertikal, dioptimalkan untuk mobilitas petugas (operator di lapangan/atap rumah sakit).
- **Indikator Visual Cepat**: Harus ada pengenalan status yang instan. 
  - Status CRITICAL (< 30%) berwarna Merah cerah.
  - Komponen kartu (cards) berukuran besar dan mudah ditekan (*finger-friendly*).

### Adaptasi Arsitektur Project Sebelumnya (Evolusi PL)
- **Modular Navigation**: Sama seperti memisahkan rute secara modular, aplikasi React Native akan menggunakan struktur Navigasi yang dikelompokkan (contoh: `AuthStack` untuk *login*, `MainTabNavigator` untuk *monitoring*).
- **Komponen UI Terpusat**: Menggunakan *wrapper component* seperti `ScreenLayout` (analoginya `PublicLayout`) yang menangani *Header* global dan *safe-area* layar secara konsisten.
- **Mekanisme Interaksi Bebas Tumpukan**: Menerapkan *single-lock mechanism* (mirip pada galeri interaktif *project* referensi) saat menekan kartu peringatan atau membuka *Bottom Sheet* grafik tangki. Hal ini mencegah pengguna menumpuk banyak jendela *modal* secara bersamaan.

### Scope Halaman Mobile App
Berdasarkan *requirements*, halaman minimal yang harus ada pada aplikasi:
1. **Layar Login**: Autentikasi operator (RBAC).
2. **Beranda (Home / Monitoring View)**: Ringkasan seluruh tangki dalam format *list* atau *grid* ringkas. Fokus menonjolkan tangki yang sedang bermasalah (WARNING/CRITICAL).
3. **Layar Peringatan (Alerts & Notifications)**: Daftar riwayat kondisi kritis lengkap dengan waktu kejadian dan status penanganan (*resolved*/*active*).
4. **Detail Tangki (Statistik)**: Informasi level air spesifik, lokasi tangki, dan grafik sederhana tren pemakaian 24 jam.
