# Panduan Pengembangan (Developer Guideline) - Web Dashboard

Panduan ini dibuat khusus untuk anggota tim yang baru pertama kali mengerjakan proyek Web Next.js. Semua setup tingkat lanjut akan dilakukan oleh Lead, Anda cukup mengikuti langkah instalasi ini untuk mulai *coding*.

## 1. Persiapan Lingkungan (Prerequisites)
Pastikan komputer Anda sudah terpasang:
- **Node.js** (LTS terbaru, misal v20+).
- **PNPM** (*Package manager* wajib proyek ini). Jika belum, *install* via npm: `npm install -g pnpm`.
- **Git** untuk *version control*.

## 2. Instalasi Proyek
1. *Clone repository* web ke lokal komputer Anda:
   ```bash
   git clone <URL_REPO_WEB>
   cd repo-web
   ```
2. Instal semua dependensi proyek menggunakan pnpm:
   ```bash
   pnpm install
   ```

## 3. Menjalankan Mode Pengembangan
Jalankan server *development*:
```bash
pnpm dev
```
Buka *browser* dan akses `http://localhost:3000`. Jika Anda mengubah kode (pada folder `app/`, `pages/`, atau komponen), perubahan akan langsung terlihat seketika (*Hot Reloading*).

## 4. Aturan Penulisan (Coding Guidelines)
- **Modular Component**: Jangan menulis seluruh kode halaman dalam satu file raksasa. Pecah kode menjadi komponen-komponen kecil (misal: `TankCard.tsx`, `Sidebar.tsx`, `LiquidGauge.tsx`) di dalam folder komponen.
- **Styling**: Gunakan kelas bawaan dari **Tailwind CSS**.
- **Branching**: Selalu buat *branch* baru dari `dev` dengan format penamaan `feature/nama-fitur` atau `fix/nama-bug`. **Jangan pernah *push* langsung ke `main`!** Wajib melalui proses Pull Request (PR).

## 5. Pemanfaatan AI (Cursor / Copilot / ChatGPT)
Proyek ini sudah dilengkapi dengan file khusus `action.md` yang bertindak sebagai "doktrin" arsitektur untuk AI. 

Jadi, ketika developer di tim Anda membuka chat AI (seperti GitHub Copilot, Cursor, atau ChatGPT/Claude via unggah file), Anda **cukup berkata**:

> *"Baca dan pahami file action.md, lalu tolong buatkan UI komponen TankCard dengan indikator warna yang sesuai!"*

Seketika itu juga, AI akan otomatis mempelajari konteks dan arsitektur proyek WP-4 tanpa Anda harus bersusah payah menjelaskan ulang aturan kerangka kerja tim kita.
