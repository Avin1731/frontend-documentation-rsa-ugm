# Security & AAA (Autentikasi, Autorisasi, Akunting) - Mobile

Keamanan sisi aplikasi *smartphone* berpedoman pada pola Tiga A (AAA) yang terhubung langsung melalui *endpoint* pengaman BFF Next.js.

## 1. Authentication ("Who are you?")
- **Client Auth via BFF**: Aplikasi melempar parameter login (*Username*, *Password*, dan MFA) ke rute `/api/auth` milik BFF.
- **Penyimpanan Secure Token**: Aplikasi tidak memanfaatkan *cookies*, melainkan menyandikan token sesi yang didapat di dalam penampung enkripsi sistem operasi (misalnya `SecureStore` Expo atau `EncryptedSharedPreferences`). Token ini dikunci dan tidak bisa diakses aplikasi lain.

## 2. Authorization ("What are you allowed to do?")
Sistem membaca dan mengelola 5 *Role* utama (ADMIN, OPERATOR, ENGINEER, MANAGEMENT, VIEWER) berdasarkan *payload* token untuk menyembunyikan atau menampilkan elemen UI:
- Elemen *Bottom Sheet* untuk memicu *Toggle Switch* kontrol pompa hanya diaktifkan jika operator terdeteksi memiliki hak akses **OPERATOR** atau **ADMIN**.
- Menu tab profil/pengaturan tidak akan menampilkan opsi konfigurasi *threshold* batas air tangki kecuali bagi **ADMIN**.

## 3. Accounting ("What did the user do?")
- **Audit Trail**: Meskipun operator menekan tombol pompa atau merevisi konfigurasi melalui *smartphone*, instruksi tersebut (*Waktu, Username, Target, Aksi*) akan dilaporkan secara akurat ke *server* BFF untuk dibukukan secara absolut dalam tabel log. 
- Menjaga prinsip integritas data dan memastikan tidak ada aksi jarak jauh dari *Mobile App* yang "luput" dari catatan historis sistem keamanan RSA UGM.
