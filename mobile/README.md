# 📱 Mobile App WP-4: Sistem Pemantauan Level Air

Selamat datang di repositori Aplikasi Mobile (Android) untuk proyek riset **Sistem Informasi Pemantauan dan Pengendalian Level Air Berbasis IoT di RSA UGM**. Repositori ini didedikasikan sepenuhnya untuk mengembangkan aplikasi *smartphone* reaktif (*React Native*) bagi para operator lapangan rumah sakit.

## 📂 Struktur Dokumentasi (Wajib Dibaca)
Bagi seluruh rekan *developer* yang terlibat dalam pembuatan UI/UX di Repo ini, Anda diwajibkan meninjau panduan spesifik ini sebelum berkontribusi:

1. **[Kebutuhan Proyek (Requirements)](./requirements.md)**: Gambaran besar fitur, lingkup interaksi, dan notifikasi ponsel.
2. **[Panduan Developer (Guideline)](./guideline.md)**: Cara melakukan instalasi `pnpm`, dan panduan pengetesan aplikasi *real-time* via aplikasi *Expo Go*.
3. **[AI Actions & Prompting](./action.md)**: Kalimat *prompt* *copy-paste* andalan untuk memastikan bantuan AI Anda (*ChatGPT/Claude*) menghasilkan *code* yang patuh arsitektur.
4. **[Tech Stack](./Techstack.md)**: Rincian spesifik React Native, NativeWind, dan konsep *fetching* data ringan dari BFF Web.
5. **[Arsitektur](./Architecture.md)**: Pemisahan Navigasi (*Stack* dan *Tab*) dan komponen *ScreenLayout*.
6. **[Scope Halaman](./Scope.md)**: Rincian daftar halaman vertikal, prinsip *finger-friendly*, dan *sorting* tangki.
7. **[Security & AAA](./Security-AAA.md)**: Penggunaan ketat `SecureStore` (Dilarang *AsyncStorage*!) dan pembedaan UI dari sisi Role.

> **Catatan Integrasi**: Aplikasi Mobile ini dikhususkan berinteraksi dengan URL **BFF Next.js** (berada di Repositori Web), dan **BUKAN** meminta langsung dari *backend* utama WP-3. Pastikan server BFF rekan Web Anda menyala saat mengetes (*fetch*) koneksi login atau histori grafik!
