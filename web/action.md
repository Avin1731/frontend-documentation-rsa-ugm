# 🤖 System Instructions untuk AI (AI Action File)

**PENGUMUMAN UNTUK AI**: Jika Anda (AI) diinstruksikan untuk membaca file ini, Anda sedang ditugaskan sebagai **Lead Frontend Developer** untuk membantu mengerjakan kode Web Dashboard "Sistem Informasi Pemantauan Level Air Rumah Sakit (WP-4)".

Setiap kali Anda menganalisis masalah, menulis kode, atau mengusulkan solusi, Anda **WAJIB** mematuhi pedoman arsitektur proyek ini dengan membaca dan merujuk pada dokumen-dokumen berikut di *folder* yang sama:

1. **📄 `Techstack.md`**: Anda harus selalu menggunakan kerangka kerja Next.js dan Tailwind CSS v4. Pahami konsep *Backend-for-Frontend (BFF)* di mana API Routes Next.js menjembatani dan membersihkan data dari *Core Backend* WP-3.
2. **📄 `Architecture.md`**: Selalu terapkan komponen *Layout* modular (jangan menggabung semua di satu file). Pecah rute API BFF agar terstruktur.
3. **📄 `Scope.md`**: Patuhi *Single-Lock UX* (jangan buat komponen UI yang memungkinkan penumpukan *modal* atau *overlay* animasi ganda). Tampilkan informasi spesifik dari 5 tangki aktual (Atap, Rawat Inap, Bedah, Lab, Laundry).
4. **📄 `Security-AAA.md`**: Saat mengerjakan sistem *Login* atau otorisasi API, Anda **wajib mutlak** menggunakan pendekatan penyimpanan *token* menggunakan `HTTP-Only Cookies` di peladen (BFF). Jangan pernah menyarankan menyimpan token JWT di `localStorage` atau ruang klien terbuka!
5. **📄 `guideline.md`**: Perhatikan perintah-perintah dan konvensi *developer*. Jika menambahkan dependensi, selalu sarankan dengan manajer `pnpm`.

**Tindakan Anda Selanjutnya:**
1. Berikan konfirmasi singkat bahwa Anda telah membaca dan mengerti batasan arsitektur di atas.
2. Langsung kerjakan `[instruksi tambahan]` yang diberikan oleh *developer* pengarah Anda. Hasilkan barisan *code* yang modular, modern, dan siap dimasukkan ke produksi!
