# 📱 Mobile App WP-4: Sistem Pemantauan Level Air

Selamat datang di repositori Aplikasi Mobile (Android) untuk proyek riset **Sistem Informasi Pemantauan dan Pengendalian Level Air Berbasis IoT di RSA UGM**. Repositori ini didedikasikan sepenuhnya untuk mengembangkan aplikasi *smartphone* reaktif bagi para operator lapangan rumah sakit.

## 🚀 Keputusan Teknis Final
Aplikasi ini dikembangkan dengan pendekatan modern dan efisien, sesuai dengan kesepakatan final arsitektur:
- **Framework Utama**: **React Native via Expo** (Mempermudah *development loop* dan kemudahan *build* rilis).
- **Styling**: Native StyleSheet / NativeWind (Tailwind).
- **State Management**: **Zustand** (Standar state realtime kita, sinkron dengan proyek Web).
- **Grafik**: **react-native-chart-kit** (Performa terbaik untuk grafik mobile).
- **Notifikasi**: **Expo Push Notifications / FCM** (Untuk dukungan *Background Push Notifications* sistem kritis).

## 📂 Struktur Dokumentasi (Wajib Dibaca)
Bagi seluruh rekan *developer* UI/UX di Repo ini, Anda diwajibkan meninjau panduan spesifik berikut sebelum berkontribusi:

1. **[Kebutuhan Proyek (Requirements)](./requirements.md)**: Gambaran besar fitur, lingkup interaksi, dan spesifikasi *Background Push Notification*.
2. **[Panduan Developer (Guideline)](./guideline.md)**: Cara melakukan instalasi `pnpm`, dan pengetesan aplikasi *real-time* via aplikasi *Expo Go*.
3. **[AI Actions & Prompting](./action.md)**: Kalimat *prompt* andalan agar bantuan AI (*ChatGPT/Claude*) menghasilkan *code* yang patuh arsitektur.
4. **[Tech Stack](./Techstack.md)**: Rincian spesifik Expo, NativeWind, dan konsep *fetching* data ringan dari BFF Web.
5. **[Arsitektur](./Architecture.md)**: Pemisahan Navigasi (*Stack* dan *Tab*) dan komponen *ScreenLayout*.
6. **[Scope Halaman](./Scope.md)**: Rincian daftar halaman vertikal, prinsip *finger-friendly*, dan *sorting* prioritas tangki kritis.
7. **[Security & AAA](./Security-AAA.md)**: Penggunaan ketat `SecureStore` (Dilarang *AsyncStorage*!) dan pembedaan UI dari sisi Role.

> **Catatan Integrasi**: Aplikasi Mobile ini dikhususkan berinteraksi dengan URL **BFF Next.js** (berada di Repositori Web), dan **BUKAN** meminta langsung dari *backend* utama WP-3. Pastikan server BFF rekan Web Anda menyala saat mengetes koneksi API, login, atau notifikasi!
