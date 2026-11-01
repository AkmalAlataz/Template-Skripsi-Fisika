# Manajemen Proyek LaTeX

Setelah LaTeX dan Visual Studio Code berhasil dikonfigurasi, tahap berikutnya adalah memahami cara mengelola berkas dalam proyek LaTeX.

Repository ini menggunakan pendekatan **single-file project**, yaitu seluruh bagian skripsi ditulis dalam satu file utama bernama `main.tex`.

Dokumentasi ini membahas pengorganisasian berkas, pengelolaan gambar, referensi, dan berkas hasil kompilasi.

Pengguna tidak perlu memahami Git atau GitHub untuk mengikuti bagian ini.

---

## 1. Struktur Dasar Proyek

Proyek skripsi menggunakan struktur direktori seperti berikut:

```text
Skripsi/
│
├── .vscode/
│   ├── settings.json
│   └── extensions.json
│
├── main.tex
├── references.bib
├── figures/
│   ├── gambar1.png
│   └── gambar2.png
│
├── .gitignore
│
└── [berkas pendukung template UGM]
```

Setiap bagian memiliki fungsi yang berbeda.

| Berkas/Folder | Fungsi |
|---|---|
| `.vscode/` | Menyimpan konfigurasi Visual Studio Code |
| `main.tex` | Dokumen utama yang memuat seluruh bagian skripsi |
| `references.bib` | Database referensi apabila menggunakan BibTeX |
| `figures/` | Menyimpan gambar dan ilustrasi |
| `.gitignore` | Mengatur berkas yang diabaikan oleh Git |
| Berkas pendukung template | Menyediakan class, package, dan aset template skripsi |

Struktur ini dapat disesuaikan dengan berkas yang disediakan oleh template skripsi UGM.

## 2. Dokumen Utama (main.tex)

Seluruh bagian skripsi ditulis dalam satu file `main.tex`.

Dokumen ini memuat bagian awal, isi skripsi, dan bagian akhir sesuai struktur yang ditentukan oleh template skripsi.

Sebagai gambaran, susunan dokumen dapat dituliskan sebagai berikut:

```latex
\documentclass{ugmskripsi}

% Package dan konfigurasi dokumen
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage[hidelinks]{hyperref}

\begin{document}

% Bagian awal skripsi
% Halaman judul, abstrak, daftar isi, dan sebagainya

\chapter{PENDAHULUAN}

% Isi bab pendahuluan

\chapter{DASAR TEORI}

% Isi bab dasar teori

\chapter{METODOLOGI PENELITIAN}

% Isi metodologi penelitian

\chapter{HASIL DAN PEMBAHASAN}

% Isi hasil dan pembahasan

\chapter{KESIMPULAN}

% Isi kesimpulan

% Bagian akhir skripsi
% Daftar pustaka dan lampiran

\end{document}
```

Kode tersebut hanya merupakan ilustrasi susunan dokumen. Pengguna tetap harus mengikuti aturan penulisan dan struktur yang disediakan oleh template skripsi UGM.

**Keuntungan pendekatan single-file:**

- Seluruh isi skripsi dapat dikelola dari satu dokumen.
- Tidak perlu mengatur pemanggilan file bab menggunakan `\input` atau `\include`.
- Struktur proyek lebih sederhana.
- Pengguna dapat langsung mencari dan mengedit bagian skripsi melalui satu file utama.

## 3. Pengelolaan Gambar

Gambar sebaiknya dikelompokkan dalam satu direktori khusus agar mudah ditemukan dan dikelola.

Contoh struktur:

```text
Skripsi/
├── main.tex
└── figures/
    ├── diagram.pdf
    ├── hasil-simulasi.png
    └── sistem-molekul.png
```

Pastikan package `graphicx` tersedia dalam konfigurasi dokumen. Apabila belum disediakan oleh class skripsi, tambahkan pada preamble:

```latex
\usepackage{graphicx}
```

Gambar dapat dipanggil menggunakan:

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[
        width=0.8\textwidth
    ]{figures/hasil-simulasi.png}
    \caption{Contoh hasil simulasi.}
    \label{fig:hasil-simulasi}
\end{figure}
```

### Hindari Absolute Path

Jangan menggunakan alamat direktori yang hanya berlaku pada komputer tertentu.

Contoh yang tidak disarankan:

```latex
\includegraphics{
    /Users/nama/Skripsi/figures/hasil.png
}
```

Gunakan relative path:

```latex
\includegraphics{
    figures/hasil.png
}
```

Dengan demikian, proyek dapat dipindahkan ke komputer lain tanpa harus mengubah lokasi gambar di dalam source LaTeX.

## 4. Pengelolaan Referensi

Berkas referensi dapat disimpan dalam database bibliografi berekstensi `.bib`.

Contoh struktur:

```text
Skripsi/
├── main.tex
└── references.bib
```

Contoh entri BibTeX:

```bibtex
@article{knizia2013intrinsic,
    author  = {Knizia, Gerald},
    title   = {Intrinsic Atomic Orbitals},
    journal = {Journal of Chemical Theory and Computation},
    year    = {2013}
}
```

Referensi kemudian dipanggil melalui perintah sitasi yang sesuai dengan sistem bibliografi pada template.

Contoh:

```latex
\cite{knizia2013intrinsic}
```

Apabila template menggunakan perintah sitasi lain, seperti `\citep`, ikuti sintaks yang telah disediakan oleh template tersebut.

Database referensi dapat dikelola menggunakan aplikasi seperti Zotero, kemudian diekspor ke format BibTeX apabila diperlukan.

## 5. Berkas Hasil Kompilasi

Ketika melakukan kompilasi, LaTeX menghasilkan beberapa berkas tambahan yang digunakan dalam proses pengelolaan dokumen.

Contohnya:

```text
main.aux
main.log
main.fdb_latexmk
main.fls
main.synctex.gz
main.toc
main.out
```

Fungsi beberapa berkas tersebut:

| Ekstensi | Fungsi |
|---|---|
| `.aux` | Menyimpan informasi referensi silang |
| `.log` | Menyimpan catatan proses kompilasi |
| `.fls` | Menyimpan daftar berkas input dan output |
| `.fdb_latexmk` | Menyimpan informasi dependensi kompilasi |
| `.synctex.gz` | Menyimpan informasi sinkronisasi source dan PDF |
| `.toc` | Menyimpan informasi daftar isi |
| `.out` | Menyimpan informasi hyperlink |

Berkas tersebut dihasilkan secara otomatis dan tidak perlu diedit secara manual.

Repository ini telah menyediakan `.gitignore` untuk mengabaikan berkas auxiliary tertentu apabila pengguna menggunakan Git.

## 6. Membersihkan Berkas Auxiliary

Apabila ingin membersihkan berkas hasil kompilasi, gunakan fitur LaTeX Workshop.

Langkah-langkah:

1. Buka Command Palette.
2. Cari `LaTeX Workshop: Clean up auxiliary files`.
3. Jalankan perintah tersebut.

Pada pengaturan repository ini, proses clean menggunakan `latexmk -c`.

Perintah tersebut membersihkan berkas auxiliary tanpa menghapus source utama maupun PDF hasil kompilasi.

Contoh berkas yang tetap dipertahankan:

```text
main.tex
main.pdf
references.bib
```

## 7. Penggunaan Relative Path

Agar proyek dapat digunakan pada komputer yang berbeda, gunakan relative path untuk memanggil gambar dan berkas pendukung lainnya.

Contoh yang tidak disarankan:

```latex
\input{
    /Users/nama/Skripsi/dokumen.tex
}
```

Pada workflow single-file repository ini, seluruh isi skripsi tetap ditulis dalam `main.tex`, sehingga pemanggilan file bab menggunakan `\input` atau `\include` tidak diperlukan.

Untuk gambar, gunakan:

```latex
\includegraphics{figures/diagram.png}
```

Hindari penggunaan alamat direktori yang bergantung pada lokasi komputer tertentu.

## 8. Penamaan Berkas

Gunakan nama berkas yang sederhana dan konsisten.

Contoh yang disarankan:

```text
main.tex
references.bib
diagram-sistem.pdf
hasil-simulasi.png
ilustrasi-molekul.png
```

Hindari penggunaan terlalu banyak spasi atau karakter khusus pada nama berkas.

Contoh yang kurang disarankan:

```text
Hasil Simulasi Final (Revisi 3).png
```

Lebih baik:

```text
hasil-simulasi-revisi3.png
```

Penamaan yang konsisten membantu mengurangi potensi masalah ketika berkas dipanggil melalui source LaTeX.

## 9. Backup Proyek

Source LaTeX merupakan berkas teks yang dapat disimpan dan dipindahkan dengan mudah.

Lakukan backup secara berkala terhadap keseluruhan folder proyek, termasuk:

- `main.tex`
- Database referensi `.bib`.
- Direktori gambar.
- Berkas class dan package yang diperlukan.
- Berkas pendukung template.

Beberapa media backup yang dapat digunakan adalah penyimpanan cloud, hard disk eksternal, atau repository Git pribadi.

Git dan GitHub bukan persyaratan untuk menggunakan konfigurasi LaTeX dalam panduan ini.

## 10. Checklist Pengelolaan Proyek

Sebelum melanjutkan penulisan skripsi, pastikan:

- [ ] Seluruh bagian skripsi ditulis dalam `main.tex`.
- [ ] Dokumen dapat dikompilasi menggunakan LaTeX Workshop.
- [ ] Gambar disimpan dalam direktori yang terorganisasi.
- [ ] Pemanggilan gambar menggunakan relative path.
- [ ] Database referensi tersimpan dengan baik.
- [ ] Tidak terdapat absolute path pada source LaTeX.
- [ ] Berkas auxiliary tidak diedit secara manual.
- [ ] Backup proyek dilakukan secara berkala.

Setelah memahami pengelolaan proyek, pengguna dapat melanjutkan ke dokumentasi **Troubleshooting** untuk mengatasi masalah yang umum terjadi ketika menggunakan LaTeX dan Visual Studio Code.