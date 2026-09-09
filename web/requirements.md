# Kebutuhan Proyek (Requirements) - Web Dashboard

Dokumen ini merupakan penjabaran kebutuhan spesifik untuk sub-tim Web (WP-4).

## 1. Lingkup Proyek (Project Scope)
Membangun antarmuka Web Dashboard berbasis Next.js (BFF) yang akan diakses melalui monitor oleh pengawas di rumah sakit. Dashboard ini bertugas untuk memantau ketinggian level air pada berbagai tangki secara terpusat.

## 2. Kebutuhan Fungsional (Functional Requirements)
- **Monitoring Real-time**: Menampilkan level air (persentase & estimasi volume) pada tangki-tangki (Tangki Atap, Rawat Inap, Bedah, Lab, Laundry).
- **Backend-for-Frontend (BFF)**: Menyediakan API Routes (Next.js) yang memformat JSON dari WP-3 dan melayani kebutuhan endpoint *client*.
- **Manajemen Peringatan (Alarm)**: Menampilkan panel peringatan visual (merah/kuning) saat sensor mendeteksi batas kritis (<30%) atau *warning* (30-60%).
- **Visualisasi Histori**: Menyajikan grafik fluktuasi level air selama 24 jam terakhir.
- **Autentikasi (AAA)**: Memiliki halaman login dan validasi berbasis Role-Based Access Control (RBAC).

## 3. Kebutuhan Non-Fungsional
- **Keamanan**: Penggunaan HTTP-Only Cookies untuk penyimpanan token sesi di sisi BFF (kebal dari celah XSS).
- **Performa**: Grafik 24 jam dan *update* data tidak boleh membuat *browser lag* (hindari *rendering* berganda/animasi bertumpuk).
- **Resolusi**: Dioptimalkan untuk tampilan *ultrawide*.

## 4. Rencana Opsional (Opsional/TBD)
- Kontrol aktuator pompa manual (ON/OFF) via API.
- Manajemen konfigurasi *threshold* batas bawah dan atas.
- Tombol *Emergency Stop*.
