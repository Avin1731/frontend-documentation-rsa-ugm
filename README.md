# 🏥 SI-POTA RSA UGM — Master Knowledge Base & Documentation
### Sistem Informasi Pemantauan Tangki Air Rumah Sakit Berbasis IoT (RSA UGM)

Repositori ini adalah pusat dokumentasi teknis (*Single Source of Truth*) untuk seluruh pengembangan antarmuka pengguna (Frontend Web & Mobile App) yang terhubung ke Backend Core Pemantauan Tangki Air RSA UGM.

---

## 📌 Alur & Hierarki Dokumentasi Proyek

Untuk memastikan integrasi antara Backend dan Frontend berjalan tanpa miskomunikasi, proyek ini menerapkan alur pembaruan dokumentasi berjenjang:

```
[1. Repo Core BE]
       │
       ▼
[2. PRD.md (Core Backend PRD)] ───────────────► Status: LOCKED (Read-Only)
       │
       ▼
[3. PRD-MFE.md (Master Frontend PRD)] ────────► Status: LOCKED (Read-Only)
       │
       ├────────────────────────────────┐
       ▼                                ▼
[4. web/PRD-Web.md]             [5. mobile/PRD-Mobile.md]
       │                                │
       ▼                                ▼
[6. Repo FE Web (Next.js + BFF)] [7. Repo FE Mobile (Expo / Android & iOS)]
```

### Prinsip Alur Perubahan:
1. **Repo BE $\rightarrow$ PRD.md:** Segala perubahan endpoint atau skema di Core Backend dicatat terlebih dahulu di [`PRD.md`](./PRD.md).
2. **PRD.md $\rightarrow$ PRD-MFE.md:** Penyesuaian arsitektur BFF, pemetaan rute bersama, dan standar keamanan sesi dipetakan di [`PRD-MFE.md`](./PRD-MFE.md).
3. **PRD-MFE.md $\rightarrow$ Platform PRD:** Masing-masing platform memiliki PRD turunan teknis spesifik ([`web/PRD-Web.md`](./web/PRD-Web.md) dan [`mobile/PRD-Mobile.md`](./mobile/PRD-Mobile.md)).
4. **Platform PRD $\rightarrow$ Implementasi Kode:** Pengembang di masing-masing repositori mengacu mutlak pada PRD platformnya.

---

## 📂 Struktur Repositori Dokumentasi

```text
frontend-documentation-rsa-ugm/
├── .agents/                        # Konfigurasi agentic tools & skills
├── illustrasi/                     # Foto dan diagram teknis lapangan RSA UGM
├── mobile/                         # Folder Dokumentasi Spesifik Mobile App
│   ├── PRD-Mobile.md               # PRD Teknis Lengkap React Native Expo SDK 58 & Multi-Stage CI
│   └── README.md                   # Panduan cepat mobile
├── web/                            # Folder Dokumentasi Spesifik Web Dashboard & BFF
│   ├── PRD-Web.md                  # PRD Teknis Lengkap Next.js App Router & Rute BFF
│   └── README.md                   # Panduan cepat web
├── CLAUDE.md                       # Konvensi perilaku asisten AI
├── PRD.md                          # [LOCKED] Master Backend PRD (Fastify, Timescale, MQTT)
├── PRD-MFE.md                      # [LOCKED] Master Frontend PRD (Web, Mobile & BFF Architecture)
└── README.md                       # Peta panduan master ini
```

---

## 🚀 Ringkasan Dokumen Kunci

| Dokumen | Peran & Ruang Lingkup | Tautan |
| :--- | :--- | :--- |
| **`PRD.md`** | **Core Backend Contract:** Kontrak 24 API, skema DB TimescaleDB, MQTT Ingestion, dan Warning Engine. | [Buka Dokumen](./PRD.md) |
| **`PRD-MFE.md`** | **Master Frontend:** Arsitektur BFF, pemetaan 8 fitur (F-01 s.d. F-08), WebSocket real-time, dan standar AAA. | [Buka Dokumen](./PRD-MFE.md) |
| **`web/PRD-Web.md`** | **Web & BFF:** Implementasi detail Next.js App Router, 23 rute handler BFF, Recharts, dan Tailwind v4. | [Buka Dokumen](./web/PRD-Web.md) |
| **`mobile/PRD-Mobile.md`** | **Mobile App:** Spesifikasi teknis React Native 0.88 & Expo SDK 58, Hospital Clean Light UI, Jest testing, Multi-Stage CI, sliding drawer, dan glance cards. | [Buka Dokumen](./mobile/PRD-Mobile.md) |

---

## 🔒 Kebijakan Kolaborasi & Branch Protection
* Seluruh pengerjaan fitur baru di repo Web maupun Mobile wajib menggunakan branch `feat/*` yang dicabangkan dari `dev`.
* Penggabungan ke `dev` dan `main` wajib melalui **Pull Request (PR)** dan lolos verifikasi otomatis **Continuous Integration (CI) GitHub Actions**.
