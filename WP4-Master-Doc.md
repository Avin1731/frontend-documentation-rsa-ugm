# SISTEM INFORMASI PEMANTAUAN DAN PENGENDALIAN LEVEL AIR BERBASIS IOT DI RSA UGM
> **Kode Dokumen**: WP4-Multi-Platform Dashboard (Web & Android) & AAA

## 1. Ringkasan Eksekutif (Executive Summary)
Dokumen ini merupakan panduan utama (Master Document) bagi Tim Work Package 4 (WP-4). WP-4 bertanggung jawab penuh atas Antarmuka Pengguna (User Interface) dan Keamanan Akses (AAA: Autentikasi, Autorisasi, dan Akunting) untuk aplikasi pemantauan level tangki air secara terpadu di Rumah Sakit Akademik (RSA) UGM.

Proyek ini dibangun menggunakan konsep **Backend-for-Frontend (BFF)**. BFF berperan sebagai peladen perantara yang mengambil data (via REST API dan WebSocket) dari Core Backend (WP-3), lalu mengubahnya menjadi format JSON yang sangat bersih (telah disortir) untuk dikonsumsi oleh aplikasi klien (Web dan Mobile).

### Mengapa Next.js BFF Adalah Titik Ideal (Sweet Spot)
1. **Infrastruktur Efisien**: Anda mendapatkan fungsi peladen perantara tanpa perlu mengonfigurasi server, port, atau deployment tambahan. Saat dashboard web di-deploy, API BFF otomatis ikut menyala di mesin yang sama.
2. **Sentralisasi Logika**: Jika tim WP-3 mengubah nama *field database* dari `tank_lvl` menjadi `waterVolume`, Anda hanya perlu mengganti kode di satu tempat (API Routes Next.js), tanpa perlu memperbarui kode *parsing* di aplikasi Mobile dan Web secara terpisah.
3. **Keamanan Sesi**: Next.js menangani *HTTP-only cookies* dengan sangat baik di sisi server, membuat token autentikasi (AAA) dari WP-3 lebih aman dari serangan pencurian sesi (*Cross-Site Scripting*/XSS).

## 2. Struktur Tim WP-4
Tim pengembangan WP-4 terdiri dari 4 (empat) orang yang dibagi ke dalam dua fokus repositori:
- **Tim Web (2 Orang)**: Mengelola Web Dashboard berbasis Next.js (termasuk *endpoint* API BFF).
- **Tim Mobile (2 Orang)**: Mengelola aplikasi Android berbasis React Native.

*(Catatan: Rincian spesifik Work Breakdown Structure akan diatur lebih lanjut dalam board tugas tersendiri).*

## 3. Rencana Opsional / Belum Fix (Perlu Diskusi)
Beberapa poin berikut merupakan turunan fitur dari WP-3 yang statusnya **[OPSIONAL / TBD]** (Belum Diputuskan secara final apakah akan diimplementasikan atau tidak). Agenda ini dicantumkan agar tim menyadari keberadaannya, namun **bukan prioritas utama** penyelesaian:
- **Tombol / Switch Kontrol Aktuator (Pompa & Valve)**: Menambahkan antarmuka bagi pengguna untuk menyalakan/mematikan pompa secara manual dari *dashboard* Web maupun Mobile.
- **Formulir Automation Rules**: Mengizinkan pengguna mengubah *threshold* hysteresis (batas aman tinggi dan rendah) secara *runtime* dari panel admin UI.

---

## 4. Daftar Isi Rincian Dokumen Teknis
Untuk menelusuri detail implementasi, *Tech Stack*, arsitektur komponen modular (mengadopsi rujukan *Evolusi PL*), daftar halaman rinci, serta manajemen sesi, silakan buka rincian spesifik di bawah ini yang telah dipisahkan ke dalam ekosistem masing-masing.

### 🌐 Implementasi Web Dashboard
Berkas-berkas dokumentasi spesifik untuk pengembangan Dashboard Web (Dioptimalkan untuk monitor *ultrawide*):
- 📄 [Spesifikasi Techstack Web](./web/Techstack.md) (Next.js, Tailwind CSS)
- 📄 [Arsitektur & Repositori Web](./web/Architecture.md) (Modular Routing & Layouting)
- 📄 [Scope & Daftar Halaman Web](./web/Scope.md) (Layar Monitoring, *Single-lock UI*)
- 📄 [Security & AAA Web](./web/Security-AAA.md) (Sistem *HTTP-Only Cookies*)

### 📱 Implementasi Mobile Apps (Android)
Berkas-berkas dokumentasi spesifik untuk aplikasi *smartphone* Android (Dioptimalkan untuk bentuk vertikal pada mobilitas petugas):
- 📄 [Spesifikasi Techstack Mobile](./mobile/Techstack.md) (React Native / Expo)
- 📄 [Arsitektur & Repositori Mobile](./mobile/Architecture.md) (Modular Navigation)
- 📄 [Scope & Daftar Halaman Mobile](./mobile/Scope.md) (Beranda ringkas, pengingat)
- 📄 [Security & AAA Mobile](./mobile/Security-AAA.md) (Manajemen *SecureStore* Android)
