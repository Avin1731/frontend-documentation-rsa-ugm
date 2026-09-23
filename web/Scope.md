# Scope Halaman & Workflow - Web Dashboard

Web Dashboard dirancang khusus untuk memonitor level air melalui monitor **ultrawide** di ruang pengawas. Panduan ini menjadi dasar perancangan antarmuka (wireframe) dan komponen.

## 1. Alur Kerja Pengguna (Workflow)
- **Alur Masuk (Authentication Flow)**: Halaman Login $\rightarrow$ Input Username & Password (+ MFA) $\rightarrow$ Validasi *Role* (BFF) $\rightarrow$ Masuk ke Dashboard Utama sesuai hak akses.
- **Alur Pemantauan (Monitoring Flow)**: Melihat *Overview* grid multi-tangki $\rightarrow$ Mengamati indikator visual (Persentase & Volume) $\rightarrow$ Jika tangki masuk zona *Critical* (<30%) atau *Warning*, *Banner Peringatan* mencolok akan muncul.
- **Alur Riwayat & Audit**: Buka menu *Logs* atau *Reports* $\rightarrow$ Lihat grafik 24 jam atau daftar aktivitas (*Accounting*).

## 2. Navigasi & Komponen Utama (UI Components)
- **Sidebar Navigation**: Dashboard, Tanks, Alarms, Reports, Logs, Settings, Users.
- **Tank Status Card**: Memuat nama, lokasi, persentase level, status koneksi, status pompa, dan *timestamp* terakhir.
- **Liquid Level Gauge**: Indikator visual berbentuk silinder tangki dengan warna dinamis (Hijau, Kuning, Merah).
- **Warning/Alarm Banner**: Kotak peringatan merah/kuning yang muncul otomatis untuk parameter kritis.
- **Historical Chart**: Grafik garis (*line chart*) 24 jam.

## 3. Daftar Halaman Utama (Pages)
1. **Halaman Login**: 
   - *Elemen*: Logo instansi (RSA UGM), Input Kredensial, Tombol Login, Opsi *Remember Me* & OTP (MFA).
2. **Dashboard Overview (Monitoring)**: 
   - *Elemen*: Ringkasan multi-tangki (Tank A, B, C, N) dalam format *grid card*, grafik ringkas harian, dan *Banner Notifikasi/Alarm* jika ada kondisi darurat.
3. **Detail Tangki & Statistik**: 
   - *Elemen*: Tampilan tangki berskala besar, rentang grafik historis 24 jam khusus tangki tersebut, indikator batas histeresis (*threshold*).
4. **Halaman Logs / Audit Trail**: 
   - *Elemen*: Tabel riwayat aktivitas admin/operator dan log peringatan sistem.
5. **Settings & Users (Khusus Admin)**: 
   - *Elemen*: Pengelolaan akun, penentuan *Role*, dan form penyetelan ambang batas (*threshold*) peringatan level air.

## 4. Standar Interaksi (UX)
- **Mekanisme Single-Lock**: Interaksi seperti *overlay* detail atau panel kontrol tidak dieksekusi secara tumpang tindih. Pengguna hanya dapat memfokuskan satu jendela modal dalam satu waktu.
