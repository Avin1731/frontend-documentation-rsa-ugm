# 📱 SI-POTA Mobile — Dokumentasi Pengembangan Android
### Aplikasi Saku Pemantauan Tangki Air Rumah Sakit Berbasis IoT (RSA UGM)

> **Repositori Target Pengembangan:** `frontend-mobile-rsa-ugm`  
> **Parent Documentation:** [PRD Master Frontend (`../PRD-MFE.md`)](../PRD-MFE.md) $\longleftarrow$ [PRD Core Backend (`../PRD.md`)](../PRD.md)  
> **Spesifikasi Teknis Lengkap:** [**`PRD-Mobile.md`**](./PRD-Mobile.md)

---

## 📌 Alur & Hierarki Dokumentasi

Sistem dokumentasi proyek mengadopsi prinsip *single source of truth* bertingkat:
$$\text{Core Backend (PRD.md)} \longrightarrow \text{Master Frontend (PRD-MFE.md)} \longrightarrow \text{Mobile PRD (PRD-Mobile.md)} \longrightarrow \text{Repo FE Mobile}$$

* Seluruh kebutuhan antarmuka Android dan integrasi mobile mengacu mutlak pada:  
  👉 [**`PRD-Mobile.md` (Product Requirements Document — Mobile App)**](./PRD-Mobile.md)

---

## 🚀 Ringkasan Teknis
* **Framework:** React Native 0.86.3 via Expo SDK 57
* **Bahasa:** TypeScript 6.x
* **HTTP Client:** Axios v1.20+ (terhubung ke Web BFF Next.js via IP LAN)
* **Realtime Channel:** WebSocket native (`ws://<LAN_IP>:8000/ws` ke Fastify Core)
* **State Management:** Zustand v5 (Tanks, Alerts, Auth, Devices)
* **Keamanan Kredensial:** `expo-secure-store` (Enkripsi hardware, anti-AsyncStorage)
* **Desain UI:** Dark Medical Theme (`#0A354C` & `#0B132B`), ramah sentuhan jempol (*finger-friendly*)

---

## 🛠️ Panduan Memulai Cepat (Quick Start)

```bash
# 1. Masuk ke direktori repositori mobile
cd frontend-mobile-rsa-ugm

# 2. Instalasi dependensi
npm install

# 3. Pastikan konfigurasi IP LAN di App.tsx atau src/config/env.ts sesuai IP laptop Anda
# (contoh: http://192.168.1.15:3000 untuk BFF)

# 4. Jalankan bundler Expo
npx expo start

# 5. Buka aplikasi Expo Go di HP Android Anda dan scan QR Code
# 6. Validasi kualitas kode sebelum mengajukan PR
npx tsc --noEmit && npx expo export --platform android
```

---

## 🔒 Kebijakan Git & Branch Protection
* **Branch `main` & `dev`:** Dilindungi *Branch Protection*, dilarang *direct push*.
* **Workflow:** Kerjakan di branch `feat/nama-fitur` dari `dev`, lakukan commit berkala di lokal, pastikan build lokal sukses, push ke dual-remote (`origin` & `upstream`), lalu buat Pull Request ke `dev`.
* **CI Quality Gate:** PR hanya dapat di-merge jika seluruh pipeline GitHub Actions CI berstatus hijau.
