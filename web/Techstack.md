# Techstack - Web Dashboard

## Framework Utama
- **Next.js (React Framework)**: Digunakan sebagai fondasi utama aplikasi web karena kemampuannya menyajikan *Server-Side Rendering* (SSR) dan memiliki fitur *API Routes* bawaan.
- **Tailwind CSS v4**: Digunakan sebagai *utility-first CSS framework* untuk mempercepat proses *styling* dan memastikan desain responsif dengan performa optimal.

## Backend-for-Frontend (BFF)
Proyek ini mengimplementasikan pola arsitektur **Backend-for-Frontend (BFF)** menggunakan **Next.js API Routes (Node.js runtime)**.
* **Titik Ideal (Sweet Spot)**:
  1. **Infrastruktur Efisien**: Peladen perantara BFF berjalan di *instance* yang sama dengan *frontend web*. Tidak diperlukan *server*, *port*, atau proses *deployment* tambahan.
  2. **Sentralisasi Logika**: BFF bertugas menjembatani *Core Backend* (WP-3) dengan *Client*. BFF mengambil data dari WP-3, memformat struktur JSON (misalnya mengubah field *raw*), dan menyediakannya dalam bentuk siap pakai untuk Web dan Mobile.

## Pustaka Tambahan
- **State Management**: React Context atau library ringan seperti Zustand.
- **Visualisasi Data**: Recharts atau Chart.js (untuk menampilkan rentang waktu riwayat log 24 jam).
- **HTTP Client**: Axios atau Fetch API (untuk berkomunikasi dengan BFF).


