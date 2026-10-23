# 📘 Panduan Setup, Clone, & Standar Workflow Pengembangan (FE & BE)

Dokumen ini disusun sebagai panduan komprehensif bagi developer baru/pemula agar dapat mengkloning, menjalankan secara lokal, dan berkontribusi pada repositori **Backend (`backend-rsa-ugm`)** maupun **Frontend Web/BFF (`frontend-web-rsa-ugm`)** dengan alur Git yang benar dan terstandarisasi.

---

## 🛠️ 1. Persiapan Environment Global di Laptop

Sebelum menyentuh repositori, pastikan software pendukung berikut sudah terpasang di laptop:

### A. Git
- **Unduh & Pasang:** Kunjungi [git-scm.com](https://git-scm.com/) lalu instal versi terbaru.
- **Konfigurasi Identitas:** Buka terminal/PowerShell dan jalankan:
  ```bash
  git config --global user.name "Nama Lengkap Anda"
  git config --global user.email "email-anda@example.com"
  ```

### B. Node.js (Versi 22 LTS Wajib)
- Proyek Frontend & Backend menggunakan fitur terbaru dan pnpm v11 yang mensyaratkan **Node.js ≥ 22.13**.
- **Unduh & Pasang:** Kunjungi [nodejs.org](https://nodejs.org/) dan pilih installer Node.js v22.
- **Verifikasi Instalasi:**
  ```bash
  node -v
  # Pastikan output menampilkan v22.x.x
  ```

### C. pnpm (Package Manager)
Proyek ini **wajib** menggunakan `pnpm` (bukan `npm` atau `yarn`) agar dependensi terisolasi rapi dan kompatibel dengan lockfile repositori.
- **Instalasi:**
  ```bash
  npm install -g pnpm
  ```
- **Verifikasi:**
  ```bash
  pnpm -v
  # Menampilkan versi pnpm
  ```

### D. Docker Desktop (Untuk Backend Database & Broker)
Backend RSA UGM membutuhkan PostgreSQL (TimescaleDB), Redis, dan Mosquitto MQTT broker.
- **Unduh & Pasang:** Kunjungi [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) lalu pasang dan pastikan aplikasinya berjalan (*running*).

---

## 🖥️ 2. Tips Penting: Buka Terminal Terpisah (Multi-Terminal)

Karena Frontend dan Backend adalah dua proyek yang berjalan berdampingan, **sangat disarankan membuka 2 atau 3 jendela Terminal / Tab PowerShell terpisah di VS Code**:

```
🖥️ Terminal 1 (Backend Terminal):
   Aktif di folder: C:\laragon\www\frontend-rsa-ugm\backend-rsa-ugm

🖥️ Terminal 2 (Frontend Terminal):
   Aktif di folder: C:\laragon\www\frontend-rsa-ugm\frontend-web-rsa-ugm

🖥️ Terminal 3 (Git & Task Terminal - Opsional):
   Digunakan khusus untuk perintah git checkout, branch, pull, test lint, dll.
```

> ⚠️ **Catatan Fatal untuk Pemula:**
> Jangan menjalankan perintah `pnpm install` atau `pnpm run dev` milik Frontend saat terminal Anda masih berada di folder Backend (atau sebaliknya).
> **Selalu pastikan prompt terminal menunjukkan folder proyek yang sesuai sebelum mengetik perintah!**

---

## 🚀 3. Panduan Step-by-Step Clone & Menjalankan Project

> 💡 **Rekomendasi Urutan:** Jalankan **Backend (BE)** terlebih dahulu agar database dan endpoint API siap saat Frontend (FE) mencoba melakukan request.

```
📁 Root Folder Kerja (Contoh: C:\laragon\www\frontend-rsa-ugm\)
  ├── backend-rsa-ugm/
  └── frontend-web-rsa-ugm/
```

---

### Step 1: Menjalankan Backend (`backend-rsa-ugm`)

1. **Buka Terminal 1, masuk ke root folder kerja lalu clone repositori:**
   ```bash
   # Masuk ke folder kerja utama
   cd C:\laragon\www\frontend-rsa-ugm

   # Clone repositori backend
   git clone https://github.com/PMLD-RSA/backend-rsa-ugm.git
   
   # WAJIB MASUK KE FOLDER BACKEND:
   cd backend-rsa-ugm
   ```

2. **Pastikan berada di branch `dev`:**
   ```bash
   git checkout dev
   git pull origin dev
   ```

3. **Install dependensi:**
   ```bash
   pnpm install
   ```

4. **Siapkan Environment File (`.env`):**
   Salin file template `.env.example` menjadi `.env`:
   ```bash
   cp .env.example .env
   # Pada Windows PowerShell jika 'cp' error:
   # Copy-Item .env.example .env
   ```

5. **Catatan Dockerfile (Bagi yang menjalankan via Docker Image):**
   Jika backend dibuild menjadi image Docker, pastikan file `Dockerfile` pada baris ke-29 menyalin folder `docs`:
   ```dockerfile
   # Stage 2 (Runner)
   COPY --from=builder /app/dist ./dist
   COPY docs ./docs   # <-- Pastikan baris ini ada agar swagger / file docs terbawa ke container
   ```

6. **Nyalakan Database & Layanan Penunjang (Docker):**
   *(Pastikan Docker Desktop sudah running)*
   ```bash
   docker compose up -d timescaledb redis mosquitto
   ```

7. **Migrasi & Inisialisasi Database:**
   ```bash
   pnpm run db:push
   pnpm run init-db
   ```

8. **Jalankan Backend dalam Mode Development:**
   ```bash
   pnpm run dev
   ```
   > 🟢 Backend aktif di: `http://localhost:8000`  
   > 📑 Dokumentasi Swagger API: `http://localhost:8000/documentation`  
   > *Biarkan Terminal 1 ini tetap terbuka dan berjalan.*

---

### Step 2: Menjalankan Frontend Web / BFF (`frontend-web-rsa-ugm`)

1. **Buka Terminal 2 (Terminal Baru), clone repositori Frontend:**
   ```bash
   # Masuk ke folder kerja utama
   cd C:\laragon\www\frontend-rsa-ugm

   # Clone repositori frontend web
   git clone https://github.com/PMLD-RSA/frontend-web-rsa-ugm.git

   # WAJIB MASUK KE FOLDER FRONTEND:
   cd frontend-web-rsa-ugm
   ```

2. **Pastikan berada di branch `dev`:**
   ```bash
   git checkout dev
   git pull origin dev
   ```

3. **Install dependensi:**
   ```bash
   pnpm install
   ```

4. **Siapkan Environment File (`.env.local`):**
   Next.js membaca file `.env.local` untuk konfigurasi lokal:
   ```bash
   cp .env.example .env.local
   # Pada Windows PowerShell jika 'cp' error:
   # Copy-Item .env.example .env.local
   ```

5. **Jalankan Frontend Web:**
   ```bash
   pnpm run dev
   ```
   > 🟢 Akses Dashboard di browser: 👉 `http://localhost:3000`  
   > Kredensial Login Dev:
   > - **Admin:** `admin` / `admin123`
   > - **Operator:** `operator` / `op123`
   > - **Viewer:** `viewer` / `view123`  
   > *Biarkan Terminal 2 ini tetap terbuka dan berjalan.*

---

## 🌿 4. Alur Kerja Git & Aturan Branch (SOP Developer)

Untuk menjaga kode tidak rusak dan mencegah konflik antar developer, seluruh tim wajib mengikuti alur di bawah ini:

### 📐 Hirarki & Pohon Branch
```
[main]          <-- Branch Rilis Produksi (Diproteksi ketat, dilarang coding langsung)
  │
[dev]           <-- Branch Integrasi Utama (Semua fitur bermuara ke sini)
  │
  ├── feat/nama-fitur-a   <-- Cabang kerja Anda
  └── feat/nama-fitur-b
```

> ⚠️ **Aturan Emas:**
> 1. `main` digunakan sebagai acuan `dev`.
> 2. `dev` digunakan untuk membuat cabang fitur (`feat/*`).
> 3. **JANGAN PERNAH** ngoding langsung di branch `main` atau `dev`!
> 4. Seluruh pengerjaan fitur/perbaikan wajib di branch baru bertipe `feat/*` atau `fix/*`.

---

### 🔄 Siklus Pengerjaan Fitur Baru (Step-by-Step)

#### 1. Selaraskan `dev` Lokal Sebelum Mulai
Buka terminal di folder proyek terkait (FE atau BE), lalu tarik update terbaru:
```bash
git checkout dev
git pull origin dev
```

#### 2. Buat Branch Baru untuk Fitur
Gunakan penamaan yang deskriptif: `feat/nama-fitur` atau `fix/nama-bug`:
```bash
git checkout -b feat/tampilan-grafik-tangki
```

#### 3. Ngoding & Cek Status Secara Berkala
Untuk melihat file apa saja yang berubah:
```bash
git status
```

#### 4. Wajib Uji Kualitas Sebelum Commit (Quality Gate Lokal)
Sebelum commit atau push, pastikan kode Anda tidak ada error:
```bash
pnpm run lint        # Memeriksa standar kode / ESLint
npx tsc --noEmit     # Memeriksa tipe TypeScript
pnpm run build       # Memastikan bundle produksi berhasil
```
> 🛑 Jika salah satu perintah di atas gagal (merah/error), **PERBAIKI DULU**. Jangan dipush dalam keadaan error!

#### 5. Commit Menggunakan Format Conventional Commits
Format standar commit: `<tipe>(<scope>): <keterangan singkat>`:
```bash
git add .
git commit -m "feat(tank): implementasi grafik riwayat sensor 24 jam"
```

#### 6. Push Branch Anda ke GitHub
```bash
git push -u origin feat/tampilan-grafik-tangki
```
> 💡 *Catatan:* Repositori ini sudah dilengkapi CI otomatis pada event `push`. Begitu Anda push branch `feat/...`, GitHub Actions langsung berjalan menguji kode Anda. Anda bisa memantau status centang hijau di GitHub sebelum membuat PR!

#### 7. Buka Pull Request (PR) ke `dev`
1. Buka repositori di GitHub.
2. Klik tombol **Compare & pull request**.
3. **PENTING:** Pastikan **Base branch = `dev`** (Bukan `main`!).
4. Tunggu pengecekan otomatis **GitHub Actions CI Quality Gate**.
5. Jika CI sudah berstatus **HIJAU (PASS)** 🟢, PR siap direview dan di-merge ke `dev`.

#### 8. Rilis ke `main` (Setelah `dev` Stabil)
Setelah serangkaian fitur di `dev` teruji dan siap dirilis:
- Buat PR dari **`dev` -> `main`**.
- Pastikan CI di `main` juga berstatus **HIJAU (PASS)** sebelum di-merge.

---

## 📝 5. Panduan Standar Format Commit (Conventional Commits)

Gunakan tipe commit yang sesuai agar riwayat proyek rapi dan mudah dilacak:

| Tipe | Kapan Digunakan | Contoh Pesan Commit |
|---|---|---|
| `feat` | Menambahkan fitur atau halaman baru | `feat(alerts): tambah tombol aksi resolve alert` |
| `fix` | Memperbaiki bug atau error | `fix(auth): perbaiki redirect saat session expired` |
| `docs` | Mengubah atau menambah dokumentasi | `docs: perbarui panduan instalasi di README` |
| `style` | Merapikan format tampilan (CSS, Tailwind, spacing) | `style(sidebar): sesuaikan padding navigasi mobile` |
| `refactor` | Mengubah struktur kode tanpa merubah fungsi | `refactor(proxy): sederhanakan handler fallback mock` |
| `chore` | Update dependensi, konfigurasi CI, atau build script | `chore(ci): upgrade node runner ke versi 22` |

---

## 💡 6. Tips Mengatasi Masalah Umum Pemula

1. **"Saya lupa pindah branch dan terlanjur ngoding di `dev`!"**
   - Tenang, JANGAN panik dan JANGAN commit!
   - Cukup jalankan perintah ini untuk memindahkan perubahan yang belum di-commit ke branch baru:
     ```bash
     git checkout -b feat/fitur-saya-yang-terlanjur
     ```
   - Semua perubahan otomatis aman berpindah ke branch baru.

2. **"Branch lokal saya ketinggalan jauh dari remote!"**
   - Selaraskan kembali branch lokal Anda:
     ```bash
     git checkout dev
     git fetch --all
     git pull origin dev
     ```

3. **"Tidak bisa push karena rejected (non-fast-forward)!"**
   - Biasanya karena ada commit baru di remote yang belum ditarik ke lokal.
   - Solusi: Lakukan `git pull origin <nama-branch>` terlebih dahulu, selesaikan konflik (jika ada), lalu push kembali.
