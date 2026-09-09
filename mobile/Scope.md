# Scope Halaman & Workflow - Mobile App (Android)

Antarmuka Mobile dirancang untuk layar sentuh berorientasi **vertikal (portrait)**, dengan penekanan pada responsivitas dan komponen UI berukuran besar (*finger-friendly*) untuk mobilitas operator.

## 1. Alur Kerja Pengguna (Workflow)
- **Alur Masuk (Authentication Flow)**: Halaman Login $\rightarrow$ Input kredensial (+ MFA) $\rightarrow$ Validasi *Role* via BFF $\rightarrow$ Beranda Monitoring.
- **Alur Pemantauan (Monitoring Flow)**: *Scroll* *Overview* daftar tangki $\rightarrow$ Sistem secara otomatis menempatkan tangki berstatus *Critical* / *Warning* di urutan paling atas $\rightarrow$ Operator mengamati *Liquid Level Gauge* dan volume.
- **Alur Kontrol Manual (Opsional / TBD)**: Pilih tangki dari daftar $\rightarrow$ Buka *Bottom Sheet* kontrol $\rightarrow$ *Swipe* atau tekan Toggle pompa $\rightarrow$ Verifikasi otorisasi $\rightarrow$ Tindakan terekam otomatis di log.
- **Alur Riwayat Khusus Mobile**: Buka menu peringatan $\rightarrow$ Lihat daftar alarm (*active*/*resolved*).

## 2. Navigasi & Komponen Utama (UI Components)
- **Bottom Tabs / Drawer**: Home (Dashboard), Tanks, Alarms, Profile/Settings.
- **Tank Status Card (Mobile)**: Kartu ringkas dengan tata letak vertikal memuat *Liquid Level Gauge*, lokasi, *badge status*, dan *timestamp*.
- **Warning/Alarm Banner**: *Toasts* atau *Snackbar* peringatan yang muncul melayang (mengambang) di bagian atas/bawah layar jika ada tangki kritis.

## 3. Daftar Halaman Utama (Pages)
1. **Layar Login**: 
   - *Elemen*: Logo instansi RSA UGM, form input, opsi *remember me*, dan MFA.
2. **Beranda Monitoring (*List/Grid*)**: 
   - *Elemen*: Ringkasan kartu multi-tangki (Atap Gedung Utama, Rawat Inap, Bedah, dll). *Sorting* otomatis berdasarkan tingkat keparahan (*Severity*).
3. **Layar Peringatan (Alarms & Notifications)**: 
   - *Elemen*: Daftar *list-view* untuk riwayat alarm lengkap dengan keterangan waktu dan status penanganan.
4. **Detail Tangki (*Bottom Sheet / Modal*)**: 
   - *Elemen*: Pemaparan tangki secara penuh, indikator volume, dan *line chart* (grafik) ringkas 24 jam.
   - *(Jika disetujui)*: Panel saklar aktuator (ON/OFF) dan *Emergency Stop Button* yang mencolok.

## 4. Standar Interaksi (UX)
- **Mekanisme *Single-Lock* (Bebas Tumpuk)**: Penguncian navigasi apabila pengguna membuka *Bottom Sheet* atau pop-up detail tangki. Hal ini mencegah pengguna menumpuk banyak jendela yang dapat memberatkan memori *smartphone*.
