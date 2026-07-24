# 🔐 Client-Side OTP Generator (2FA / TOTP)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![No Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen.svg)]()
[![100% Client-Side](https://img.shields.io/badge/Environment-100%25%20Client--Side-purple.svg)]()

Aplikasi web ringan untuk menghasilkan kode **Two-Factor Authentication (2FA)** atau **Time-Based One-Time Password (TOTP)** langsung di browser Anda. 

Dibuat sepenuhnya menggunakan **HTML, CSS, dan Vanilla JavaScript murni** (tanpa pustaka eksternal seperti jQuery atau Node.js crypto), memanfaatkan standar **Web Crypto API** bawaan browser yang sangat aman.

---

## ✨ Fitur Utama

* **100% Privasi & Client-Side:** Seluruh proses perhitungan kriptografi dilakukan di peramban Anda. *Secret Key* tidak pernah dikirim ke server mana pun.
* **Tanpa Dependensi (Zero Dependencies):** Kode sangat ringan, cepat, dan mudah dipahami karena hanya menggunakan bahasa web standar.
* **Indikator Waktu Real-Time:** Dilengkapi dengan *progress bar* visual dan hitung mundur 30 detik sesuai standar RFC 6238.
* **Smart Cooldown:** Tombol *Generate OTP* tetap aktif secara visual namun mencegah pemanggilan ulang yang tidak perlu selama masa jeda 30 detik berlangsung. Kode OTP terakhir tetap dipertahankan di layar sebagai referensi bahkan saat hitung mundur waktu habis.
* **Salin Cepat (Copy to Clipboard):** Menyalin kode 6-digit ke *clipboard* hanya dengan satu klik disertai notifikasi interaktif.
* **Penyimpanan Lokal:** *Secret key* Anda disimpan di `localStorage` peramban Anda, sehingga Anda tidak perlu mengetikkannya berulang kali saat membuka aplikasi kembali.
* **Desain Responsif & Modern:** Antarmuka dengan *gradient* berestetika modern yang tampil rapi di layar desktop maupun perangkat seluler.

---

## 🚀 Memulai Generate OTP

Aplikasi ini berjalan 100% di sisi klien, sehingga Anda cukup membuka file `index.html` di peramban modern Anda (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari, dll) dan ikuti langkah berikut:

1. Klik tombol **⚙️ 2FA Secret** di sudut kanan atas.
2. Masukkan **Secret Key** 2FA Anda (dalam format Base32 standar, contoh: `JBSWY3DPEHPK3PXP`).
3. Klik **Simpan**.
4. Klik tombol **Generate OTP**. Kode 6-angka akan muncul di layar beserta *timer* hitung mundur 30 detik!

---

## 🛠️ Cara Kerja & Teknologi (Under the Hood)

Aplikasi ini menerapkan standar industri **RFC 6238 (TOTP)** dan **RFC 4226 (HOTP)** melalui tahapan berikut:

1. **Base32 Decoding:** *Secret Key* dari pengguna di-decode dari format string Base32 menjadi `Uint8Array` agar dapat diproses secara kriptografis.
2. **Time Counter:** Waktu sistem (*Epoch timestamp*) dibagi dengan interval standar **30 detik** untuk menghasilkan angka penghitung (*counter*) 8-byte dalam format *big-endian*.
3. **HMAC-SHA1 Encryption:** Menggunakan metode asinkron dari standar peramban `window.crypto.subtle.sign` untuk menghasilkan tanda tangan kriptografi HMAC-SHA1 berbasis *secret key* dan *time counter*.
4. **Dynamic Truncation:** Hasil *hash* 20-byte dipotong secara dinamis menggunakan *bitwise operations* untuk menghasilkan angka bilangan bulat, lalu diambil modulo **1.000.000** untuk menghasilkan tepat **6 digit kode OTP**.

---

## 🔒 Catatan Keamanan & Privasi

* **Penyimpanan LocalStorage:** Aplikasi ini menyimpan *Secret Key* di dalam `localStorage` browser Anda untuk kemudahan penggunaan. Pastikan Anda tidak menggunakan aplikasi ini di komputer umum atau perangkat yang dapat diakses oleh pihak yang tidak berwenang.
* **Tanpa Server Berarti Tanpa Risiko Kebocoran Jaringan:** Karena tidak ada *backend*, *Secret Key* Anda aman dari intersepsi jaringan (*Man-in-the-Middle Attack* ke server aplikasi).

---

## 🤝 Kontribusi

Kontribusi, saran, dan laporan *bug* sangat dipersilakan! Silakan buat *Issue* baru atau kirimkan *Pull Request* apabila Anda memiliki ide untuk meningkatkan performa atau tampilan aplikasi ini.

---

## 📝 Lisensi

Proyek ini didistribusikan di bawah lisensi **MIT**. Anda bebas untuk menggunakan, memodifikasi, dan mendistribusikan kode ini untuk keperluan pribadi maupun komersial. Lihat file `LICENSE` untuk detail lebih lanjut.

tentunya source code ini dibuat pake AI dalam waktu 5 menit
