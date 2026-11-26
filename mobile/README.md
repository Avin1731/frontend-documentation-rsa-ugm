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
* **Framework:** React Native 0.88.1 via Expo SDK 58 (`~58.0.26`)
* **Library UI:** React 19.3.0
* **Bahasa:** TypeScript ~6.0.3
* **Ikonografi & Font:** `@expo/vector-icons` ^15.0.2 (Feather) & `expo-font` ~58.0.12 (bebas emoji)
* **HTTP Client:** Axios ^1.21.1 (terhubung ke Web BFF Next.js via IP LAN / Tailscale)
* **Realtime Channel:** WebSocket native (`ws://<HOST_IP>:8000/ws?token=<jwt>` ke Fastify Core)
* **State Management:** Zustand ^5.1.0 (Tanks, Alerts, Auth, Devices, Reports, AuditLogs, Users) dengan selector granular
* **Keamanan Kredensial:** Expo SecureStore ~58.0.3 (Enkripsi hardware Keystore/Keychain, anti-AsyncStorage)
* **Unit Testing:** Jest ^30.5.2 & ts-jest ^29.4.15 (11 suites / 58 tests dengan metrik coverage)
* **CI Quality Gate:** GitHub Actions Single-Pipeline (`typecheck`, `test:ci`, `expo-doctor`, `expo export`)
* **Desain UI & Performa:** Design Tokens selaras Figma Web (`#0A3F5C`, `#05004E`, `#FECB28`, `#ECF4F9`, `#E4002B`), lambang resmi UGM, Skeleton loader, animasi native-driver (`useReducedMotion`), dan virtualisasi `FlatList`

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
