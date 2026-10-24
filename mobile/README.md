# 📱 SI-POTA Mobile — Dokumentasi Pengembangan Mobile App
### Aplikasi Saku Pemantauan Tangki Air Rumah Sakit Berbasis IoT (RSA UGM)

> **Repositori Target Pengembangan:** `frontend-mobile-rsa-ugm`  
> **Parent Documentation:** [PRD Master Frontend (`../PRD-MFE.md`)](../PRD-MFE.md) $\longleftarrow$ [PRD Core Backend (`../PRD.md`)](../PRD.md)  
> **Spesifikasi Teknis Lengkap:** [**`PRD-Mobile.md`**](./PRD-Mobile.md)

---

## 📌 Alur & Hierarki Dokumentasi

Sistem dokumentasi proyek mengadopsi prinsip *single source of truth* bertingkat:
$$\text{Core Backend (PRD.md)} \longrightarrow \text{Master Frontend (PRD-MFE.md)} \longrightarrow \text{Mobile PRD (PRD-Mobile.md)} \longrightarrow \text{Repo FE Mobile}$$

* Seluruh kebutuhan antarmuka Android/iOS dan integrasi mobile mengacu mutlak pada:  
  👉 [**`PRD-Mobile.md` (Product Requirements Document — Mobile App)**](./PRD-Mobile.md)

---

## 🚀 Ringkasan Teknis
* **Framework:** React Native 0.88.0 via Expo SDK 58 (`~58.0.19`)
* **Library UI:** React 19.3.0
* **Bahasa:** TypeScript ~6.0.3
* **HTTP Client:** Axios ^1.20.0 (terhubung ke Web BFF Next.js via IP LAN / Tailscale)
* **Realtime Channel:** WebSocket native (`ws://<HOST_IP>:8000/ws` ke Fastify Core)
* **State Management:** Zustand ^5.0.16 (Tanks, Alerts, Auth, Devices)
* **Keamanan Kredensial:** Expo SecureStore ~58.0.2 (Enkripsi hardware Keystore/Keychain, anti-AsyncStorage)
* **Unit Testing:** Jest ^30.5.2 & ts-jest ^29.4.15 (Automated unit tests dengan metrik coverage)
* **CI Quality Gate:** GitHub Actions Multi-Stage Pipeline (3 Chained Stages: Healthcheck $\rightarrow$ Unit Tests $\rightarrow$ Dry Export)
* **Desain UI:** Hospital Clean Light Theme (`#F8FAFC`, `#FFFFFF`, `#E2E8F0`, `#0F172A`, `#0A354C`), dot badges semantik, dan area sentuh ramah sentuhan jempol ($\ge 44 \times 44\text{ dp}$)

---

## 🛠️ Panduan Memulai Cepat (Quick Start)

```bash
# 1. Masuk ke direktori repositori mobile
cd frontend-mobile-rsa-ugm

# 2. Instalasi dependensi
npm install

# 3. Salin file konfigurasi environment
cp .env.example .env
# Buka .env dan uncomment target host yang sesuai (contoh: IP LAN WiFi laptop Anda)

# 4. Jalankan bundler Metro Expo
npx expo start

# 5. Buka aplikasi Expo Go di HP Anda dan scan QR Code
# 6. Validasi kualitas kode sebelum mengajukan PR
npm run typecheck && npm test && npx expo-doctor && npx expo export --no-bytecode
```

---

## 🔒 Kebijakan Git & Branch Protection
* **Branch `main` & `dev`:** Dilindungi *Branch Protection*, dilarang *direct push*.
* **Workflow:** Kerjakan di branch `feat/*`, `ci/*`, atau `fix/*` dari `dev`, lakukan commit berkala di lokal, pastikan seluruh pengujian lokal sukses, push ke dual-remote (`origin` & `upstream`), lalu buat Pull Request ke `dev`.
* **CI Quality Gate:** PR hanya dapat di-merge jika seluruh 3 tahapan Multi-Stage CI GitHub Actions lolos berstatus hijau.
