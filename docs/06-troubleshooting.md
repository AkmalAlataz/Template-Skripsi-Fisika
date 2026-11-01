# Troubleshooting

Bagian ini membahas beberapa masalah yang umum terjadi ketika menggunakan LaTeX dan Visual Studio Code.

Sebelum melakukan perubahan konfigurasi, periksa terlebih dahulu pesan kesalahan yang ditampilkan oleh LaTeX Workshop. Pesan tersebut biasanya memberikan petunjuk mengenai sumber masalah.

---

## 1. LaTeX Workshop Tidak Ditemukan

**Gejala:** Perintah seperti `Build LaTeX project` tidak muncul di Command Palette.

**Penyebab:** Extension LaTeX Workshop belum terpasang atau belum aktif.

**Solusi:**

1. Buka Extensions pada Visual Studio Code.
2. Cari `LaTeX Workshop`.
3. Pastikan extension dari James Yu sudah terpasang dan aktif.
4. Apabila baru selesai memasang extension, muat ulang Visual Studio Code.

Gunakan Command Palette untuk mencari perintah:

```text
LaTeX Workshop: Build LaTeX project
```

## 2. LaTeX Compiler Tidak Ditemukan

**Gejala:** Proses kompilasi gagal dan muncul pesan seperti:

```text
spawn latexmk ENOENT
```

atau:

```text
latexmk: command not found
```

**Penyebab:** LaTeX Workshop tidak dapat menemukan program `latexmk`.

**Solusi:**

Pastikan distribusi LaTeX sudah terpasang dan `latexmk` tersedia pada sistem.

Buka terminal, kemudian jalankan:

```bash
which latexmk
```

Pada Windows, gunakan:

```powershell
where latexmk
```

Apabila lokasi program tidak ditemukan, periksa kembali instalasi distribusi LaTeX dan konfigurasi `PATH` sistem.

Jika `latexmk` sudah terpasang tetapi masih tidak ditemukan oleh VS Code, periksa konfigurasi compiler pada:

```text
.vscode/settings.json
```

Pastikan alamat program yang digunakan sesuai dengan lokasi instalasi pada komputer.

## 3. Dokumen Tidak Menghasilkan PDF

**Gejala:** Proses build dijalankan, tetapi file PDF tidak dihasilkan atau tidak diperbarui.

**Penyebab yang mungkin:**

- Terdapat kesalahan sintaks pada source LaTeX.
- Terdapat package atau class yang tidak ditemukan.
- Compiler tidak dapat menyelesaikan proses kompilasi.
- Konfigurasi dokumen utama tidak sesuai.

**Solusi:**

1. Buka panel Output pada Visual Studio Code.
2. Pilih `LaTeX Workshop` pada daftar kanal output.
3. Periksa pesan kesalahan yang muncul.
4. Perbaiki kesalahan pada file `main.tex`.
5. Jalankan kembali proses build.

Perhatikan pesan yang diawali dengan tanda berikut:

```text
!
```

Contoh:

```text
! LaTeX Error: Missing $ inserted.
```

Pesan tersebut menunjukkan bahwa terdapat kesalahan pada penulisan sintaks LaTeX.

Jangan hanya berpatokan pada pesan kesalahan terakhir. Periksa juga beberapa baris sebelumnya karena pesan awal biasanya lebih dekat dengan sumber masalah.

## 4. Class Template UGM Tidak Ditemukan

**Gejala:** Muncul pesan:

```text
LaTeX Error: File `ugmskripsi.cls' not found.
```

**Penyebab:** LaTeX tidak dapat menemukan class yang digunakan oleh dokumen.

**Solusi:**

Pastikan berkas class dan seluruh berkas pendukung template UGM tersedia pada direktori proyek sesuai struktur template aslinya.

Periksa bagian awal `main.tex`:

```latex
\documentclass{ugmskripsi}
```

Nama class pada perintah tersebut harus sesuai dengan berkas class yang disediakan oleh template.

Jangan menghapus atau memindahkan berkas pendukung template secara sembarangan karena beberapa berkas mungkin dibutuhkan selama proses kompilasi.

## 5. Package LaTeX Tidak Ditemukan

**Gejala:** Muncul pesan seperti:

```text
LaTeX Error: File `nama-package.sty' not found.
```

**Penyebab:** Package yang dipanggil dalam dokumen belum tersedia pada distribusi LaTeX.

**Solusi:**

Periksa nama package yang disebutkan pada pesan kesalahan.

Selanjutnya, pastikan distribusi LaTeX telah terpasang dengan paket yang diperlukan.

- **TeX Live / MacTeX:** Periksa ketersediaan package melalui pengelola paket TeX Live.
- **MiKTeX:** Periksa pengelolaan paket melalui MiKTeX Console.

Setelah package tersedia, jalankan kembali kompilasi dokumen.

## 6. Gambar Tidak Muncul

**Gejala:** Kompilasi gagal dengan pesan seperti:

```text
LaTeX Error: File `gambar.png' not found.
```

atau gambar tidak muncul pada PDF.

**Penyebab yang mungkin:**

- Nama file tidak sesuai.
- Lokasi gambar salah.
- Ekstensi file tidak sesuai.
- Penulisan relative path tidak benar.

**Solusi:**

Pastikan gambar berada pada direktori yang sesuai.

Contoh struktur:

```text
Skripsi/
├── main.tex
└── figures/
    └── gambar.png
```

Kemudian panggil gambar menggunakan:

```latex
\includegraphics{figures/gambar.png}
```

Periksa kembali nama file, termasuk penggunaan huruf besar dan kecil.

Sebagai contoh, `Gambar.png` dan `gambar.png` dapat dianggap sebagai dua nama file yang berbeda.

## 7. Sitasi atau Daftar Pustaka Tidak Muncul

**Gejala:** Sitasi tidak muncul pada dokumen atau daftar pustaka tidak terbentuk dengan benar.

**Penyebab yang mungkin:**

- Database referensi tidak ditemukan.
- Citation key tidak sesuai.
- Sistem bibliografi belum berjalan dengan benar.
- Dokumen belum dikompilasi ulang setelah perubahan referensi.

**Solusi:**

Periksa beberapa hal berikut:

1. Pastikan file database `.bib` tersedia pada lokasi yang dipanggil oleh dokumen.
2. Pastikan citation key pada perintah sitasi sesuai dengan entri di dalam file `.bib`.
3. Pastikan konfigurasi bibliografi mengikuti sistem yang digunakan oleh template.
4. Jalankan kembali proses build agar LaTeX dapat memperbarui sitasi dan daftar pustaka.

Contoh pemanggilan sitasi:

```latex
\cite{knizia2013intrinsic}
```

Pastikan entri dengan key tersebut memang tersedia pada database referensi.

Apabila template menggunakan BibTeX atau Biber, pastikan proses bibliografi yang sesuai telah dikonfigurasi.

## 8. Perubahan Source Tidak Terlihat pada PDF

**Gejala:** Source `main.tex` sudah diubah, tetapi PDF masih menampilkan hasil sebelumnya.

**Penyebab yang mungkin:**

- Proses build belum selesai.
- Kompilasi gagal sehingga PDF tidak diperbarui.
- PDF yang dibuka bukan hasil kompilasi terbaru.
- Terdapat masalah pada proses pembaruan preview.

**Solusi:**

1. Jalankan kembali `Build LaTeX project`.
2. Tunggu hingga proses kompilasi selesai.
3. Periksa apakah terdapat pesan kesalahan pada Output.
4. Buka kembali PDF melalui preview LaTeX Workshop.

Pastikan proses build berhasil sebelum menyimpulkan bahwa perubahan source tidak diterapkan.

## 9. PDF dan Source Tidak Sinkron

**Gejala:** Ketika memilih bagian tertentu pada PDF, Visual Studio Code tidak berpindah ke lokasi source yang sesuai, atau sebaliknya.

**Penyebab:** Informasi sinkronisasi antara source LaTeX dan PDF belum diperbarui atau tidak tersedia.

**Solusi:**

Pastikan konfigurasi compiler menggunakan opsi SyncTeX.

Pada konfigurasi `latexmk`, opsi berikut digunakan untuk mengaktifkannya:

```text
-synctex=1
```

Pastikan proses build telah berhasil dan file:

```text
main.synctex.gz
```

dihasilkan.

Apabila masalah masih terjadi, jalankan kembali proses kompilasi.

## 10. Proses Kompilasi Mengalami Masalah

**Gejala:** Proses build berhenti, hasil kompilasi tidak diperbarui, atau masalah tetap muncul setelah source diperbaiki.

**Solusi:**

Salah satu langkah yang dapat dilakukan adalah membersihkan berkas auxiliary.

1. Buka Command Palette.
2. Cari perintah:

```text
LaTeX Workshop: Clean up auxiliary files
```

3. Jalankan perintah tersebut.
4. Lakukan build ulang menggunakan:

```text
LaTeX Workshop: Build LaTeX project
```

Berkas auxiliary akan dibuat kembali ketika proses kompilasi berlangsung.

Jangan menghapus `main.tex`, database referensi, gambar, atau berkas pendukung template ketika membersihkan proyek.

## 11. VS Code Tidak Menemukan Dokumen Utama

**Gejala:** LaTeX Workshop tidak dapat menemukan dokumen utama atau mengompilasi file yang tidak sesuai.

**Penyebab:** Folder yang dibuka pada Visual Studio Code bukan direktori utama proyek skripsi.

**Solusi:**

Pastikan pengguna membuka seluruh folder proyek melalui:

```text
File → Open Folder
```

Pilih direktori yang berisi `main.tex`, bukan hanya membuka file `main.tex` secara terpisah.

Struktur direktori yang benar memiliki file utama pada lokasi berikut:

```text
Skripsi/
├── .vscode/
├── main.tex
├── references.bib
└── figures/
```

Dengan membuka folder proyek, konfigurasi `.vscode` dapat diterapkan dan LaTeX Workshop dapat mengenali berkas pendukung lainnya.

---

## 12. Langkah Pemeriksaan Umum

Apabila mengalami masalah yang belum tercantum pada dokumentasi ini, lakukan pemeriksaan secara berurutan:

1. Pastikan distribusi LaTeX telah terpasang.
2. Pastikan extension LaTeX Workshop aktif.
3. Pastikan folder proyek dibuka dengan benar.
4. Pastikan `main.tex` dapat ditemukan.
5. Pastikan seluruh berkas pendukung template tersedia.
6. Periksa pesan kesalahan pada panel Output.
7. Bersihkan berkas auxiliary jika diperlukan.
8. Jalankan kembali proses build.

Apabila masalah masih belum terselesaikan, catat pesan kesalahan yang muncul dan periksa file `.log` hasil kompilasi. Informasi tersebut dapat membantu mengidentifikasi sumber masalah dengan lebih spesifik.

---

## 13. Checklist Akhir

Sebelum menggunakan template untuk penulisan skripsi, pastikan seluruh konfigurasi berikut telah berfungsi:

- [ ] Distribusi LaTeX telah terpasang.
- [ ] Extension LaTeX Workshop telah aktif.
- [ ] Compiler `latexmk` dapat ditemukan oleh sistem.
- [ ] File `main.tex` dapat dikompilasi.
- [ ] PDF berhasil dihasilkan.
- [ ] Gambar dapat ditampilkan.
- [ ] Sitasi dan daftar pustaka dapat dihasilkan.
- [ ] Sinkronisasi source dan PDF berfungsi.
- [ ] Berkas auxiliary dapat dibersihkan melalui LaTeX Workshop.

Dengan demikian, konfigurasi LaTeX dan Visual Studio Code telah siap digunakan untuk mendukung proses penulisan skripsi menggunakan template Fisika UGM.