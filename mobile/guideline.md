# Panduan Pengembangan (Developer Guideline) - Mobile App

Panduan ini ditujukan bagi anggota tim yang baru mulai menyentuh proyek aplikasi ponsel pintar (Android) menggunakan React Native (Expo). Setup infrastruktur berat akan di-*handle* oleh *Lead*, Anda cukup mengikuti panduan instalasi ini untuk mulai koding.

## 1. Persiapan Lingkungan (Prerequisites)
Pastikan komputer Anda terpasang:
- **Node.js** (LTS terbaru, misal v20+).
- **PNPM** (*Package manager* wajib proyek ini, instal via terminal: `npm install -g pnpm`).
- **Git** untuk *version control*.
- Ponsel Android dengan aplikasi **Expo Go** terinstal dari *Play Store* (untuk *testing* langsung di ponsel).

## 2. Instalasi Proyek
1. *Clone repository* aplikasi Mobile ke lokal komputer Anda:
   ```bash
   git clone <URL_REPO_MOBILE>
   cd repo-mobile
   ```
2. Instal semua dependensi:
   ```bash
   pnpm install
   ```

## 3. Menjalankan Mode Pengembangan
Mulai server pengembangan Expo:
```bash
pnpm start
```
Sebuah *QR Code* akan muncul di terminal. **Scan QR Code** tersebut menggunakan aplikasi **Expo Go** dari ponsel pintar Anda. *Syarat mutlak: PC dan Ponsel harus terhubung ke jaringan WiFi/Hotspot yang sama.* 
Setiap baris kode *React Native* yang Anda simpan akan seketika mengubah tampilan di layar ponsel Anda (*Fast Refresh*).

## 4. Aturan Penulisan (Coding Guidelines)
- **Modular Component**: Jangan tumpuk seluruh desain dalam satu file raksasa `App.js`. Pecahlah UI Anda ke folder khusus (misal: `TankCard.js`, `LiquidGauge.js`).
- **Styling**: Terapkan NativeWind/Tailwind CSS secara rapi sesuai konvensi.
- **Branching**: Selalu pisahkan cabang pekerjaan fitur (misal: `feature/login-screen`, `feature/tank-card`). Jangan pernah menyatukan (menekan *push* & *merge*) kode ke *branch* `main` secara langsung tanpa *Pull Request*.

## 5. Pemanfaatan AI (Cursor / Copilot / ChatGPT)
Proyek ini sudah dilengkapi dengan file khusus `action.md` yang bertindak sebagai "doktrin" arsitektur untuk AI. 

Jadi, ketika developer di tim Anda membuka chat AI (seperti GitHub Copilot, Cursor, atau ChatGPT/Claude via unggah file), Anda **cukup berkata**:

> *"Baca dan pahami file action.md, lalu tolong buatkan UI komponen TankCard dengan indikator warna yang sesuai!"*

Seketika itu juga, AI akan otomatis mempelajari konteks dan arsitektur proyek WP-4 tanpa Anda harus bersusah payah menjelaskan ulang aturan kerangka kerja tim kita.

## 6. Standar Penulisan Commit (Conventional Commits)
Gunakan format berikut saat melakukan commit agar riwayat proyek rapi:
- `feat: [pesan]` -> Untuk menambahkan fitur baru.
- `fix: [pesan]` -> Untuk memperbaiki bug/error.
- `docs: [pesan]` -> Untuk mengubah dokumentasi.
- `style: [pesan]` -> Untuk merapikan kode (spasi, format) tanpa ubah logika.
- `refactor: [pesan]` -> Untuk merombak kode tanpa menambah fitur atau fix bug.
- `chore: [pesan]` -> Untuk urusan maintenance (update dependencies, config).
