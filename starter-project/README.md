# Starter Project LaTeX

Folder ini merupakan proyek awal untuk menulis dokumen menggunakan LaTeX dan Visual Studio Code.

Konfigurasi di dalamnya telah disesuaikan dengan repository Template Skripsi Fisika.

## Struktur Proyek

```text
starter-project/
├── .vscode/
│   ├── settings.json
│   └── extensions.json
├── .gitignore
├── README.md
└── main.tex
```

## Cara Menggunakan

1. Salin folder `starter-project` ke lokasi proyek yang diinginkan.
2. Buka folder proyek melalui Visual Studio Code.
3. Pastikan LaTeX Workshop telah terpasang.
4. Buka `main.tex`.
5. Jalankan perintah `LaTeX Workshop: Build LaTeX project`.
6. Hasil kompilasi akan ditampilkan dalam PDF Viewer.

## Konfigurasi

Folder `.vscode` menyediakan konfigurasi workspace untuk:

- Kompilasi menggunakan `latexmk`.
- Automatic Build.
- PDF Preview.
- Forward dan Inverse SyncTeX.
- Clean Auxiliary Files.

Pastikan distribusi LaTeX telah terpasang dan executable `latexmk` tersedia melalui system PATH.

## Catatan

Dokumen `main.tex` menggunakan kelas standar `article` sebagai contoh awal.

Untuk penulisan skripsi, pengguna dapat mengganti kelas dokumen dengan template skripsi institusi masing-masing.

Template institusi tidak disertakan dalam starter project ini dan harus diperoleh melalui sumber resminya.