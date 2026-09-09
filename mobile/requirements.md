# Kebutuhan Proyek (Requirements) - Mobile App (Android)

Dokumen ini merupakan penjabaran kebutuhan spesifik untuk sub-tim Mobile (WP-4).

## 1. Lingkup Proyek (Project Scope)
Membangun aplikasi ponsel pintar (Android) berbasis React Native/Expo. Aplikasi ini khusus digunakan oleh operator lapangan rumah sakit untuk memonitor level tangki air secara dinamis dan mendapatkan peringatan instan (*alerts*).

## 2. Kebutuhan Fungsional (Functional Requirements)
- **Monitoring Portabel**: Menampilkan *list/grid* tangki air beserta *Liquid Level Gauge* persentasenya.
- **Konsumsi BFF**: Mengambil JSON dari Next.js BFF (bukan langsung dari WP-3) sehingga data lebih ringan untuk diolah oleh memori ponsel.
- **Prioritas Tampilan Tangki**: Sistem algoritma *sorting* harus meletakkan tangki berstatus CRITICAL (<30%) dan WARNING (30-60%) di daftar teratas secara otomatis.
- **Notifikasi/Peringatan**: Terdapat riwayat/daftar *alarms* khusus yang sangat jelas di layar *smartphone*.
- **Autentikasi (AAA)**: Memiliki halaman login dan membatasi akses tampilan berdasar peran (RBAC).

## 3. Kebutuhan Non-Fungsional
- **Keamanan Token**: Menyimpan token dari BFF ke dalam *SecureStore/EncryptedSharedPreferences*, dilarang menaruh di penampungan memori rentan (seperti *AsyncStorage* reguler).
- **Performa Memori**: Mencegah *memory leak* dari animasi menumpuk (wajib menerapkan metode *Single-Lock* saat membuka modal/detail tangki bawah).
- **Resolusi**: Dioptimalkan untuk orientasi *vertikal (portrait)* layar sentuh dengan ikon dan elemen berukuran (*finger-friendly*).

## 4. Rencana Opsional (Opsional/TBD)
- Kontrol aktuator pompa manual (*Toggle switch*).
- Tombol Merah *Emergency Stop* besar.
