# Konfigurasi LaTeX Workshop

LaTeX Workshop merupakan ekstensi utama yang digunakan untuk mengintegrasikan lingkungan LaTeX dengan Visual Studio Code.

Ekstensi ini memungkinkan pengguna melakukan kompilasi dokumen, melihat hasil PDF secara langsung, melakukan sinkronisasi antara source LaTeX dan PDF, serta mengelola berkas sementara hasil kompilasi.

Dokumentasi ini menjelaskan konfigurasi LaTeX Workshop yang digunakan dalam repository **Template Skripsi Fisika**.

## 1. Struktur Konfigurasi

Repository ini menyediakan konfigurasi workspace VS Code pada direktori `.vscode/`.

```text
Template-Skripsi-Fisika/
│
└── .vscode/
    ├── settings.json
    └── extensions.json
```

Berkas `settings.json` berisi pengaturan LaTeX Workshop, sedangkan `extensions.json` berisi rekomendasi ekstensi yang diperlukan.

Pengaturan workspace memungkinkan konfigurasi digunakan bersama oleh seluruh pengguna repository tanpa harus mengubah Global Settings masing-masing.

## 2. Konfigurasi Workspace

Buka berkas `.vscode/settings.json` dan masukkan konfigurasi berikut:

```json
{
    "latex-workshop.latex.outDir": "%DIR%",
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.view.pdf.viewer": "tab",

    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ]
        }
    ],

    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        }
    ],

    "latex-workshop.latex.clean.method": "command",
    "latex-workshop.latex.clean.command": "latexmk",
    "latex-workshop.latex.clean.args": [
        "-outdir=%OUTDIR%",
        "-c",
        "%TEX%"
    ],

    "latex-workshop.latex.autoClean.run": "never"
}
```

Konfigurasi tersebut dibagi menjadi beberapa bagian utama, yaitu compiler, recipe, automatic build, PDF viewer, dan clean command.

## 3. Konfigurasi Compiler

Compiler merupakan perangkat yang mengubah source LaTeX menjadi dokumen PDF.

Dalam repository ini, kita menggunakan `latexmk` sebagai pengelola proses kompilasi.

```json
"latex-workshop.latex.tools": [
    {
        "name": "latexmk",
        "command": "latexmk",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "-outdir=%OUTDIR%",
            "%DOC%"
        ]
    }
]
```

Setiap konfigurasi tool memiliki tiga komponen utama:

- `name`: nama tool yang akan digunakan dalam recipe.
- `command`: perintah executable yang dijalankan.
- `args`: argumen yang diberikan kepada executable.

### 3.1 Argumen Compiler

Berikut penjelasan setiap argumen yang digunakan:

| Argumen | Fungsi |
|---|---|
| `-synctex=1` | Mengaktifkan pembuatan informasi SyncTeX |
| `-interaction=nonstopmode` | Melanjutkan proses kompilasi tanpa berhenti pada prompt interaktif |
| `-file-line-error` | Menampilkan informasi kesalahan beserta nama file dan nomor baris |
| `-pdf` | Mengaktifkan mode keluaran PDF pada latexmk |
| `-outdir=%OUTDIR%` | Menentukan direktori penyimpanan hasil kompilasi |
| `%DOC%` | Menentukan lokasi dokumen utama tanpa ekstensi `.tex` |

Pada konfigurasi ini, compiler dipanggil menggunakan:

```json
"command": "latexmk"
```

Tanpa menggunakan lokasi executable secara absolut, seperti:

```text
/Library/TeX/texbin/latexmk
```

Pendekatan ini memungkinkan konfigurasi digunakan pada macOS maupun Windows selama executable `latexmk` tersedia melalui environment variable `PATH`.

### 3.2 Placeholder LaTeX Workshop

LaTeX Workshop menyediakan placeholder khusus yang akan digantikan secara otomatis ketika proses kompilasi dijalankan.

Beberapa placeholder yang digunakan dalam konfigurasi ini adalah:

| Placeholder | Keterangan |
|---|---|
| `%DOC%` | Lokasi dokumen utama tanpa ekstensi |
| `%DOCFILE%` | Nama dokumen utama tanpa ekstensi |
| `%DIR%` | Direktori dokumen utama |
| `%OUTDIR%` | Direktori keluaran yang ditentukan oleh konfigurasi workspace |
| `%TEX%` | Lokasi lengkap file TeX ketika menjalankan clean command |

Sebagai contoh, apabila dokumen utama berada pada:

```text
/project/examples/main.tex
```

Maka `%DOC%` akan menunjuk pada:

```text
/project/examples/main
```

Sedangkan `%DIR%` akan menunjuk pada:

```text
/project/examples
```

Placeholder memungkinkan konfigurasi compiler digunakan tanpa harus menuliskan alamat direktori secara manual.

## 4. Konfigurasi Recipe

Recipe merupakan urutan tool yang digunakan oleh LaTeX Workshop untuk membangun dokumen.

Konfigurasi recipe dalam repository ini:

```json
"latex-workshop.latex.recipes": [
    {
        "name": "latexmk",
        "tools": [
            "latexmk"
        ]
    }
]
```

Recipe tersebut hanya menggunakan satu tool, yaitu `latexmk`.

Pemanggilan recipe dilakukan melalui perintah:

`LaTeX Workshop: Build LaTeX project`

Karena hanya terdapat satu recipe, recipe tersebut menjadi pilihan utama untuk proses kompilasi.

Penggunaan `latexmk` menyederhanakan proses build karena pengelolaan pengulangan kompilasi dan pemanggilan program pendukung dilakukan oleh `latexmk`.

## 5. Automatic Build

Salah satu fitur penting LaTeX Workshop adalah kemampuan melakukan kompilasi secara otomatis ketika dokumen mengalami perubahan.

Pengaturan yang digunakan:

```json
"latex-workshop.latex.autoBuild.run": "onFileChange"
```

LaTeX Workshop menyediakan tiga pilihan automatic build:

| Mode | Perilaku |
|---|---|
| `never` | Menonaktifkan kompilasi otomatis |
| `onSave` | Mengompilasi ketika file `.tex` disimpan |
| `onFileChange` | Mengompilasi ketika perubahan pada file proyek terdeteksi |

Repository ini menggunakan `onFileChange` agar dokumen dapat dikompilasi kembali ketika perubahan terdeteksi pada berkas yang menjadi dependensi proyek.

Untuk proyek sederhana yang hanya menggunakan satu file `.tex`, perubahan pada dokumen utama akan memicu proses kompilasi ulang.

## 6. PDF Viewer

LaTeX Workshop menyediakan PDF Viewer internal yang memungkinkan hasil kompilasi ditampilkan langsung di dalam VS Code.

Pengaturan yang digunakan:

```json
"latex-workshop.view.pdf.viewer": "tab"
```

Nilai `tab` menunjukkan bahwa dokumen PDF akan ditampilkan melalui tab internal VS Code menggunakan PDF.js.

Untuk membuka hasil kompilasi:

1. Buka file `.tex` utama.
2. Tekan `Cmd + Shift + P` pada macOS atau `Ctrl + Shift + P` pada Windows.
3. Cari `LaTeX Workshop: View LaTeX PDF file`.
4. Jalankan perintah tersebut.

PDF Viewer akan menampilkan hasil kompilasi dan memperbarui tampilan setelah proses build berhasil.

## 7. Sinkronisasi Source dan PDF (SyncTeX)

SyncTeX merupakan fitur yang memungkinkan pengguna berpindah antara bagian tertentu pada source LaTeX dan lokasi yang sesuai pada dokumen PDF.

Fitur ini diaktifkan melalui argumen compiler:

```text
-synctex=1
```

LaTeX Workshop menyediakan dua jenis sinkronisasi.

### 7.1 Forward SyncTeX

Forward SyncTeX memungkinkan pengguna berpindah dari source LaTeX menuju posisi yang sesuai pada PDF.

Langkah penggunaan:

1. Buka dokumen `.tex`.
2. Letakkan kursor pada baris yang ingin diperiksa.
3. Tekan `Cmd + Option + J` pada macOS atau `Ctrl + Alt + J` pada Windows.
4. PDF Viewer akan berpindah ke posisi yang sesuai dengan kursor.

### 7.2 Inverse SyncTeX

Inverse SyncTeX memungkinkan pengguna berpindah dari dokumen PDF menuju source LaTeX.

Langkah penggunaan:

1. Buka PDF melalui internal PDF Viewer VS Code.
2. Cari bagian dokumen yang ingin diperiksa.
3. Tekan `Control` sambil mengeklik bagian tersebut.
4. VS Code akan membuka source LaTeX pada bagian yang bersesuaian.

Dengan kedua fitur tersebut, pengguna dapat melakukan pemeriksaan dokumen secara lebih efisien tanpa harus mencari halaman dan baris kode secara manual.

## 8. Membersihkan Berkas Hasil Kompilasi

Proses kompilasi LaTeX menghasilkan beberapa berkas tambahan yang diperlukan untuk pengelolaan referensi, daftar isi, informasi kesalahan, dan sinkronisasi dokumen.

Beberapa berkas yang umum dihasilkan antara lain:

| Ekstensi | Fungsi |
|---|---|
| `.aux` | Informasi referensi dan hasil kompilasi |
| `.log` | Catatan proses kompilasi |
| `.fls` | Daftar berkas masukan dan keluaran |
| `.fdb_latexmk` | Informasi dependensi dan status kompilasi latexmk |
| `.synctex.gz` | Informasi sinkronisasi source dan PDF |
| `.toc` | Informasi daftar isi |
| `.out` | Informasi keluaran hyperlink |

LaTeX Workshop menyediakan fitur untuk membersihkan berkas tambahan tersebut.

### 8.1 Konfigurasi Clean Command

```json
"latex-workshop.latex.clean.method": "command",
"latex-workshop.latex.clean.command": "latexmk",
"latex-workshop.latex.clean.args": [
    "-outdir=%OUTDIR%",
    "-c",
    "%TEX%"
]
```

Konfigurasi tersebut menggunakan `latexmk` dengan argumen:

```bash
latexmk -outdir=<OUTDIR> -c <TEX>
```

Opsi `-c` digunakan untuk membersihkan berkas tambahan hasil kompilasi tanpa menghapus dokumen PDF.

### 8.2 Automatic Clean

Repository ini menggunakan:

```json
"latex-workshop.latex.autoClean.run": "never"
```

Dengan pengaturan tersebut, berkas tambahan tidak akan dihapus secara otomatis setelah kompilasi.

Pembersihan dilakukan secara manual ketika diperlukan, sehingga file auxiliary tetap tersedia selama proses penulisan berlangsung.

### 8.3 Menjalankan Clean

Untuk membersihkan berkas tambahan:

1. Buka Command Palette.
2. Cari `LaTeX Workshop: Clean up auxiliary files`.
3. Jalankan perintah tersebut.

Hasil yang diharapkan adalah berkas tambahan seperti `.aux`, `.log`, dan `.fls` terhapus, sedangkan file `.tex` dan `.pdf` tetap tersedia.

## 9. Alur Kerja Kompilasi

Berdasarkan konfigurasi yang telah dibuat, alur kerja penulisan LaTeX dapat diringkas sebagai berikut:

```text
        Source LaTeX (.tex)
                |
                v
       Perubahan Dokumen
                |
                v
          Automatic Build
                |
                v
             latexmk
                |
                v
           pdfLaTeX
                |
                v
          Output PDF
                |
                v
          PDF Viewer
                |
                v
      Forward / Inverse SyncTeX
                |
                v
        Pemeriksaan Dokumen
```

Berkas tambahan hasil kompilasi tetap disimpan selama proses penulisan. Pengguna dapat menjalankan Clean Auxiliary Files ketika ingin membersihkannya.

## 10. Pengujian Konfigurasi

Setelah seluruh konfigurasi tersedia, lakukan pengujian berikut:

| No. | Pengujian | Hasil yang D