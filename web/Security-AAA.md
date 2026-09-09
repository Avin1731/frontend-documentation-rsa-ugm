# Security & AAA (Autentikasi, Autorisasi, Akunting) - Web

Sistem keamanan sisi *frontend* dikelola secara penuh melalui mekanisme **Backend-for-Frontend (BFF)** Next.js, menerapkan prinsip Tiga A (AAA) untuk memastikan *Confidentiality, Integrity, Availability*.

## 1. Authentication ("Who are you?")
Mengidentifikasi identitas pengguna yang mencoba masuk ke sistem.
- **Mekanisme HTTP-Only Cookies**: 
  - Kredensial divalidasi ke WP-3 via BFF. Token JWT disematkan ke dalam *cookies* (`HttpOnly`, `Secure`, `SameSite`) oleh BFF Next.js untuk mencegah pencurian token melalui celah skrip (*XSS*).
- **Form Login & MFA**: Menyediakan input kredensial (Username & Password) ditambah opsi *Multi-Factor Authentication* (MFA 6 digit) untuk pengamanan ekstra tingkat instansi medis.

## 2. Authorization ("What are you allowed to do?")
Menerapkan *Role-Based Access Control* (RBAC) di mana tampilan antarmuka (wireframe) beradaptasi secara otomatis berdasarkan *role*:
- **ADMIN**: Akses penuh ke seluruh halaman, termasuk *User Management* dan formulir konfigurasi *Threshold* batas air tangki.
- **OPERATOR**: Fokus pada layar monitoring multi-tangki dan diizinkan mengakses panel tombol kontrol pompa manual (opsional).
- **ENGINEER**: Akses diagnostik perangkat IoT dan *maintenance*.
- **MANAGEMENT**: Memiliki akses hanya untuk melihat *Dashboard* (Overview) dan laporan (*Reports*) dalam mode *Read-only*.
- **VIEWER**: Akses *Read-only* dengan informasi yang lebih terbatas.

## 3. Accounting ("What did the user do?")
Memastikan prinsip akuntabilitas di mana seluruh tindakan kritikal harus transparan dan dapat ditelusuri.
- **Audit Trail & Logs**:
  - Halaman tabel *Logs* mencatat secara detail: **[Waktu] | [Username] | [Target Tangki] | [Aksi]**.
  - Contoh rekaman aksi: `10:32 | operator01 | Tank-03 | Pump OFF -> ON` atau `10:45 | admin01 | Tank-03 | Threshold 30% -> 25%`.
  - Sistem BFF akan meneruskan setiap parameter perubahan ke *Core Backend* (WP-3) untuk memastikan catatan tersebut tidak dapat dihapus atau dimanipulasi dari klien.
