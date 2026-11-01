# Panduan Instalasi LaTeX

Dokumentasi ini menjelaskan cara memasang distribusi LaTeX pada sistem operasi macOS dan Windows.

Distribusi LaTeX yang direkomendasikan adalah:

| Sistem Operasi | Distribusi LaTeX | Compiler |
|---|---|---|
| macOS | MacTeX | pdfLaTeX |
| Windows | TeX Live | pdfLaTeX |

Kedua distribusi tersebut menyediakan perangkat yang diperlukan dalam repository ini, termasuk `latexmk`, `pdflatex`, `kpsewhich`, dan `texcount`.

---

## 1. Instalasi LaTeX pada macOS (MacTeX)

### 1.1 Mengunduh MacTeX

MacTeX merupakan distribusi LaTeX lengkap berbasis TeX Live yang telah disesuaikan untuk sistem operasi macOS.

Unduh MacTeX melalui situs resmi berikut:

https://www.tug.org/mactex/mactex-download.html

Pilih paket instalasi MacTeX (`.pkg`) versi terbaru yang tersedia.

### 1.2 Memasang MacTeX

1. Buka file `MacTeX.pkg` yang telah diunduh.
2. Ikuti petunjuk instalasi yang ditampilkan.
3. Gunakan pilihan instalasi standar.
4. Tunggu hingga proses instalasi selesai.

Instalasi standar MacTeX menyediakan distribusi TeX Live lengkap beserta perangkat pendukungnya.

MacTeX menyediakan symbolic link untuk executable LaTeX pada direktori:

```text
/Library/TeX/texbin
```

Direktori tersebut memungkinkan sistem mengakses berbagai perintah LaTeX tanpa harus menuliskan lokasi instalasi secara lengkap.

### 1.3 Memeriksa Hasil Instalasi

Setelah instalasi selesai, buka Terminal baru dan jalankan perintah berikut:

```bash
which latexmk
which pdflatex
which kpsewhich
which texcount
```

Hasil yang diharapkan menunjukkan lokasi executable pada direktori:

```text
/Library/TeX/texbin/
```

Selanjutnya, periksa versi compiler:

```bash
latexmk -v
pdflatex --version
```

Apabila kedua perintah menampilkan informasi versi, distribusi LaTeX telah berhasil dipasang.

### 1.4 Mengatasi Masalah PATH

Apabila perintah LaTeX tidak dapat ditemukan, periksa apakah direktori executable MacTeX sudah terdaftar dalam environment variable `PATH`.

Jalankan:

```bash
echo $PATH
```

Jika diperlukan, tambahkan direktori MacTeX ke konfigurasi shell Zsh dengan membuka file `~/.zprofile` dan menambahkan baris berikut:

```bash
export PATH="/Library/TeX/texbin:$PATH"
```

Simpan perubahan, kemudian buka Terminal baru dan ulangi pemeriksaan instalasi.

Apabila VS Code sedang terbuka, tutup dan buka kembali aplikasi tersebut agar perubahan PATH dapat dikenali.

---

## 2. Instalasi LaTeX pada Windows (TeX Live)

### 2.1 Mengunduh TeX Live

TeX Live merupakan distribusi LaTeX lintas sistem operasi yang dikembangkan dan dikelola oleh TeX Users Group (TUG).

Unduh installer Windows melalui tautan resmi CTAN berikut:

https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe

Installer tersebut akan mengunduh paket-paket TeX Live yang diperlukan selama proses instalasi berlangsung. Pastikan komputer terhubung ke internet.

### 2.2 Memasang TeX Live

1. Jalankan file `install-tl-windows.exe` yang telah diunduh.
2. Pilih opsi instalasi yang tersedia.
3. Buka konfigurasi lanjutan apabila ingin memeriksa pengaturan instalasi.
4. Pilih skema instalasi `scheme-full` apabila kapasitas penyimpanan mencukupi.
5. Gunakan direktori instalasi standar apabila tidak memiliki kebutuhan khusus.
6. Mulai instalasi dan tunggu hingga seluruh proses selesai.

Direktori instalasi standar untuk TeX Live 2026 adalah:

```text
C:\texlive\2026
```

Hindari penggunaan karakter non-ASCII pada direktori instalasi untuk mengurangi kemungkinan masalah kompatibilitas.

Installer TeX Live biasanya akan menambahkan direktori executable ke environment variable `PATH` Windows secara otomatis.

### 2.3 Memeriksa Hasil Instalasi

Setelah instalasi selesai, buka Command Prompt atau PowerShell baru.

Jalankan perintah berikut:

```powershell
where.exe latexmk
where.exe pdflatex
where.exe kpsewhich
where.exe texcount
```

Untuk instalasi standar, hasilnya seharusnya menunjuk ke direktori:

```text
C:\texlive\2026\bin\windows\
```

Selanjutnya, periksa versi compiler:

```powershell
latexmk -v
pdflatex --version
```

Apabila kedua perintah menampilkan informasi versi, distribusi LaTeX telah berhasil dipasang.

### 2.4 Mengatasi Masalah PATH

Apabila Windows tidak dapat mengenali perintah LaTeX:

1. Tutup dan buka kembali terminal.
2. Jalankan ulang VS Code apabila sedang terbuka.
3. Periksa pengaturan Environment Variables pada Windows.
4. Pastikan direktori executable TeX Live sudah dimasukkan ke dalam `PATH`.

Untuk instalasi standar TeX Live 2026, direktori yang perlu ditambahkan adalah:

```text
C:\texlive\2026\bin\windows
```

Apabila TeX Live dipasang pada direktori yang berbeda, sesuaikan lokasi tersebut dengan direktori instalasi sebenarnya.

---

## 3. Pemeriksaan Akhir Instalasi

Sebelum melanjutkan ke konfigurasi Visual Studio Code, pastikan seluruh executable berikut dapat diakses melalui terminal.

| Executable | Fungsi |
|---|---|
| `latexmk` | Mengelola dan mengotomatisasi proses kompilasi LaTeX |
| `pdflatex` | Mengompilasi dokumen LaTeX menjadi PDF |
| `kpsewhich` | Mencari lokasi package dan berkas konfigurasi TeX |
| `texcount` | Menghitung jumlah kata dalam dokumen LaTeX |

Keempat perintah tersebut harus dapat dijalankan melalui system `PATH`.

Perintah `latexmk` menjadi komponen utama dalam repository ini karena akan digunakan sebagai compiler untuk mengelola proses kompilasi dokumen.

**Catatan:** Apabila salah satu perintah belum dapat ditemukan, selesaikan masalah instalasi atau konfigurasi PATH terlebih dahulu sebelum melanjutkan.

---

## 4. Tahap Selanjutnya

Setelah distribusi LaTeX berhasil dipasang, lanjutkan ke dokumentasi berikutnya:

**[Konfigurasi Visual Studio Code](03-vscode-setup.md)**

Pada bagian tersebut akan dibahas:

- Instalasi Visual Studio Code.
- Instalasi ekstensi LaTeX Workshop.
- Pengaturan workspace.
- Konfigurasi compiler dan recipe.
- Kompilasi dokumen LaTeX dan PDF Preview.
- Integrasi SyncTeX.