# Techstack - Mobile App (Android)

## Framework Utama
- **React Native** (bisa menggunakan tambahan **Expo** untuk mempercepat proses kompilasi, penyiapan *environment*, dan distribusi APK secara instan).
- **Styling**: Native StyleSheet atau bisa juga mengadopsi Tailwind CSS menggunakan **NativeWind** agar konvensi penamaan *class* tetap sama dengan tim Web.

## Integrasi Data (Berinteraksi dengan BFF)
- Aplikasi Mobile **TIDAK** menembak langsung *endpoint* dari WP-3 (Core Backend). 
- Aplikasi Mobile sepenuhnya melakukan mekanisme HTTP Request terhadap *endpoint* API Routes milik Next.js BFF. 
- *Benefit*: Pemrosesan data mentah (seperti kalkulasi persentase air atau perataan struktur JSON kompleks) sudah diselesaikan oleh *server* BFF. Aplikasi Android hanya menerima JSON bersih dan siap dirender, menghemat penggunaan memori dan baterai *smartphone* petugas.

## Pustaka Tambahan
- **State Management**: Redux Toolkit atau Zustand (sangat berguna agar *state* tangki air tetap terjaga saat petugas berpindah-pindah layar secara cepat).
- **Visualisasi Grafik**: `react-native-chart-kit` atau `victory-native` untuk menampilkan grafik riwayat air yang mulus (*native-friendly*) tanpa ancaman jeda lag.


