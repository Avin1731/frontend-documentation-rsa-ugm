# 🌐 Web Dashboard & BFF — SI-POTA RSA UGM
### Dokumentasi Teknis Pengembangan Frontend Web & Backend-for-Frontend (BFF)

> **Repositori Target Pengembangan:** `frontend-web-rsa-ugm`  
> **Parent Documentation:** [PRD Master Frontend (`../PRD-MFE.md`)](../PRD-MFE.md) $\longleftarrow$ [PRD Core Backend (`../PRD.md`)](../PRD.md)  
> **Spesifikasi Teknis Lengkap:** [**`PRD-Web.md`**](./PRD-Web.md)

---

## 📌 Alur & Hierarki Dokumentasi

Sistem dokumentasi proyek mengadopsi prinsip *single source of truth* bertingkat:
$$\text{Core Backend (PRD.md)} \longrightarrow \text{Master Frontend (PRD-MFE.md)} \longrightarrow \text{Web PRD (PRD-Web.md)} \longrightarrow \text{Repo FE Web}$$

* Seluruh kebutuhan antarmuka Web dan API Routes BFF mengacu mutlak pada:
  👉 [**`PRD-Web.md` (Product Requirements Document — Web & BFF)**](./PRD-Web.md)

---

## 🚀 Ringkasan Teknis
* **Framework:** Next.js 16.3.6 (App Router)
* **Runtime Peran Ganda:**
  1. *Web Client UI* (Dashboard ruang kontrol rumah sakit untuk layar ultrawide).
  2. *Backend-for-Frontend (BFF)* (`src/app/api/*`) yang melayani klien Web dan Mobile.
* **Styling & Icons:** Tailwind CSS v4 & Lucide React.
* **State & Visualisasi:** Zustand v5 & Recharts v3.
* **Keamanan Sesi:** Cookie `HttpOnly; SameSite=Lax; Secure` (anti-XSS).
* **Port Lokal:** `http://localhost:3000`

---

## 🛠️ Panduan Memulai Cepat (Quick Start)

```bash
# 1. Masuk ke direktori repositori web
cd frontend-web-rsa-ugm

# 2. Instalasi dependensi menggunakan pnpm
pnpm install

# 3. Jalankan server development
pnpm dev

# 4. Validasi kualitas kode sebelum mengajukan PR
pnpm run lint && npx tsc --noEmit && pnpm run build
```

---

## 🔒 Kebijakan Git & Branch Protection
* **Branch `main` & `dev`:** Dilindungi *Branch Protection*, dilarang *direct push*.
* **Workflow:** Kerjakan di branch `feat/nama-fitur` dari `dev`, lakukan commit berkala di lokal, pastikan build lokal sukses, push ke dual-remote (`origin` & `upstream`), lalu buat Pull Request ke `dev`.
* **CI Quality Gate:** PR hanya dapat di-merge jika seluruh pipeline GitHub Actions CI berstatus hijau.
