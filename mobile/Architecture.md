# Architecture - Mobile App (Android)

## Topologi Repositori
Kode sumber aplikasi Android diisolasi dalam repositori khusus Mobile (terpisah dari Web BFF dan WP-3) agar memudahkan proses *build* dan rilis ke perangkat Android.

## Konsep Arsitektur Layout & Navigasi
Menyesuaikan pola arsitektur berbasis komponen modular (*layouting*) dari referensi *project* sebelumnya:
- **Modular Navigation**: Sistem rute pada *React Navigation* akan dipecah secara hierarkis (misal: `AuthStack` khusus untuk alur login dan `MainTabNavigator` untuk halaman-halaman saat operator sedang memonitor tangki).
- **Komponen Wrapper Global**: Menggunakan komponen pelapis seperti `ScreenLayout` yang berfungsi identik dengan `PublicLayout` pada *project* referensi. Komponen ini memastikan setiap layar memiliki margin *safe-area* dari OS Android dan ukuran *Header* yang konsisten di seluruh layar navigasi.

## Git Branching Strategy
- Mengikuti pola standar: `main` (aplikasi stabil rilis) -> `dev` (integrasi antar fitur) -> `feature/*` (penulisan kode baru).
- Wajib menggunakan *Pull Request* saat *merge* ke cabang utama untuk memastikan kualitas basis kode.
