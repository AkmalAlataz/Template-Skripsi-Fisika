# Konfigurasi Visual Studio Code

Setelah berhasil memasang distribusi LaTeX, tahap selanjutnya adalah menyiapkan Visual Studio Code sebagai lingkungan penulisan dan kompilasi dokumen LaTeX.

Pada tahap ini, kita akan memasang Visual Studio Code, mengintegrasikan ekstensi LaTeX Workshop, dan menggunakan konfigurasi workspace yang telah disediakan dalam repository ini.

## 1. Instalasi Visual Studio Code

### 1.1 macOS

Unduh Visual Studio Code melalui halaman resmi:

https://code.visualstudio.com/

Pilih versi macOS yang sesuai dengan perangkat:

- Apple Silicon (M1, M2, M3, dan seterusnya).
- Intel Chip.

Langkah instalasi:

1. Unduh file Visual Studio Code (`.dmg`).
2. Buka file yang telah diunduh.
3. Pindahkan `Visual Studio Code.app` ke folder `Applications`.
4. Buka Visual Studio Code melalui folder Applications.

#### Mengaktifkan perintah `code` pada Terminal

Fitur ini memungkinkan pengguna membuka direktori atau proyek langsung dari Terminal.

1. Buka Visual Studio Code.
2. Tekan `Cmd + Shift + P` untuk membuka Command Palette.
3. Cari perintah `Shell Command: Install 'code' command in PATH`.
4. Jalankan perintah tersebut.
5. Tutup dan buka kembali Terminal.

Untuk menguji instalasi, jalankan:

```bash
code --version
```

Apabila informasi versi Visual Studio Code muncul, perintah `code` sudah dapat digunakan.

### 1.2 Windows

Unduh Visual Studio Code melalui halaman resmi:

https://code.visualstudio.com/

Pilih **Windows User Installer** untuk instalasi pada akun pengguna.

Langkah instalasi:

1. Unduh installer Visual Studio Code (`.exe`).
2. Jalankan installer.
3. Ikuti petunjuk instalasi.
4. Pada bagian Additional Tasks, disarankan mengaktifkan:
   - Add to PATH.
   - Add "Open with Code" action.
   - Register Code as an editor for supported file types.
5. Selesaikan instalasi dan buka Visual Studio Code.

#### Memeriksa instalasi

Buka Command Prompt atau PowerShell dan jalankan:

```powershell
code --version
```

Apabila informasi versi muncul, Visual Studio Code telah berhasil dipasang.

Jika perintah tidak dikenali, tutup dan buka kembali terminal setelah instalasi. Periksa juga konfigurasi Environment Variables apabila masalah masih terjadi.

---

## 2. Instalasi Ekstensi LaTeX Workshop

LaTeX Workshop merupakan ekstensi utama yang digunakan untuk mengintegrasikan LaTeX dengan Visual Studio Code.

Ekstensi ini menyediakan berbagai fitur, antara lain:

- Kompilasi dokumen LaTeX.
- PDF Preview di dalam VS Code.
- Automatic Build.
- Forward dan Inverse SyncTeX.
- Autocomplete dan syntax highlighting.
- Pengelolaan proses kompilasi melalui `latexmk`.

Halaman resmi ekstensi:

https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop

### 2.1 Instalasi melalui Extensions Marketplace

1. Buka Visual Studio Code.
2. Tekan `Ctrl + Shift + X` pada Windows atau `Cmd + Shift + X` pada macOS.
3. Ketik `LaTeX Workshop` pada kolom pencarian.
4. Pastikan publisher ekstensi adalah `James Yu`.
5. Klik tombol **Install**.

Ekstensi yang benar memiliki identifier:

```text
James-Yu.latex-workshop
```

### 2.2 Instalasi melalui Terminal

Sebagai alternatif, ekstensi dapat dipasang melalui perintah berikut:

```bash
code --install-extension James-Yu.latex-workshop
```

Untuk memeriksa apakah ekstensi sudah terpasang:

```bash
code --list-extensions
```

Pastikan terdapat:

```text
james-yu.latex-workshop
```

---

## 3. Mengunduh Repository

Setelah Visual Studio Code dan LaTeX Workshop berhasil dipasang, langkah selanjutnya adalah memperoleh konfigurasi yang disediakan dalam repository ini.

Repository dapat diunduh melalui GitHub:

https://github.com/AkmalAlataz/Template-Skripsi-Fisika

### 3.1 Menggunakan Git Clone

Buka Terminal atau PowerShell, kemudian jalankan:

```bash
git clone https://github.com/AkmalAlataz/Template-Skripsi-Fisika.git
```

Masuk ke direktori repository:

```bash
cd Template-Skripsi-Fisika
```

Buka direktori tersebut menggunakan Visual Studio Code:

```bash
code .
```

### 3.2 Menggunakan Download ZIP

Apabila Git belum tersedia atau pengguna tidak ingin menggunakan Terminal:

1. Buka halaman repository GitHub.
2. Klik tombol **Code**.
3. Pilih **Download ZIP**.
4. Ekstrak file ZIP.
5. Buka Visual Studio Code.
6. Pilih `File > Open Folder`.
7. Pilih folder `Template-Skripsi-Fisika` yang telah diekstrak.

Pastikan folder yang dibuka adalah direktori utama repository, bukan hanya folder `examples` atau `docs`.

---

## 4. Mengaktifkan Rekomendasi Ekstensi

Repository ini telah menyediakan konfigurasi rekomendasi ekstensi pada:

```text
.vscode/extensions.json
```

Berkas tersebut berisi identifier ekstensi yang diperlukan:

```json
{
    "recommendations": [
        "james-yu.latex-workshop"
    ]
}
```

Ketika pengguna membuka repository untuk pertama kali, Visual Studio Code dapat menampilkan pemberitahuan untuk memasang ekstensi yang direkomendasikan.

Pilih **Install** untuk memasang LaTeX Workshop.

Apabila pemberitahuan tidak muncul:

1. Buka panel Extensions.
2. Pilih menu filter.
3. Cari bagian `Recommended`.
4. Pilih ekstensi yang direkomendasikan untuk workspace tersebut.

Pengaturan rekomendasi ekstensi ini memungkinkan setiap pengguna memperoleh daftar ekstensi yang sama tanpa harus mencarinya secara manual.

---

## 5. Menggunakan Konfigurasi Workspace

Salah satu keunggulan repository ini adalah tersedianya konfigurasi LaTeX Workshop yang dapat digunakan bersama.

Konfigurasi tersebut berada pada:

```text
.vscode/
├── settings.json
└── extensions.json
```

Berkas `settings.json` berisi pengaturan compiler, automatic build, PDF Viewer, SyncTeX, dan proses clean.

Berkas `extensions.json` berisi rekomendasi ekstensi untuk workspace.

Ketika folder repository dibuka melalui Visual Studio Code, pengaturan pada `.vscode/settings.json` akan digunakan sebagai pengaturan workspace.

Dengan demikian, pengguna tidak perlu menyalin seluruh konfigurasi ke Global Settings miliknya.

**Catatan:** konfigurasi workspace yang disediakan akan berlaku ketika folder repository dibuka sebagai workspace. Ketika membuat proyek skripsi baru di luar folder tersebut, konfigurasi workspace perlu disalin atau diterapkan kembali pada proyek baru.

---

## 6. Memeriksa Integrasi LaTeX

Sebelum mulai menulis dokumen, pastikan Visual Studio Code dapat mengenali distribusi LaTeX yang telah dipasang.

Buka Terminal di dalam Visual Studio Code, kemudian jalankan:

```bash
latexmk -v
pdflatex --version
kpsewhich --version
texcount --version
```

Pastikan seluruh perintah dapat dijalankan tanpa pesan bahwa perintah tidak ditemukan.

Apabila terdapat masalah, periksa kembali instalasi LaTeX dan konfigurasi environment variable `PATH`.

---

## 7. Pengujian Kompilasi Pertama

Untuk memastikan seluruh konfigurasi telah berjalan dengan benar, kita akan menggunakan dokumen pengujian yang tersedia dalam repository:

```text
examples/
└── main.tex
```

Langkah pengujian:

1. Buka `examples/main.tex`.
2. Pastikan ekstensi LaTeX Workshop telah aktif.
3. Tekan `Cmd + Shift + P` pada macOS atau `Ctrl + Shift + P` pada Windows.
4. Cari `LaTeX Workshop: Build LaTeX project`.
5. Jalankan perintah tersebut.
6. Tunggu hingga proses kompilasi selesai.

Apabila konfigurasi berhasil, file PDF akan dihasilkan pada direktori yang sama dengan file `.tex`.

Pengguna juga dapat melakukan pengujian berikut:

- Melakukan perubahan pada dokumen dan menyimpannya untuk menguji Automatic Build.
- Membuka PDF melalui internal PDF Viewer.
- Menguji Forward dan Inverse SyncTeX.
- Menjalankan Clean Auxiliary Files untuk membersihkan berkas sementara.

Apabila seluruh pengujian berhasil, lingkungan LaTeX di Visual Studio Code telah siap digunakan.

---

## 8. Tahap Selanjutnya

Setelah berhasil menyelesaikan instalasi dan konfigurasi awal, pengguna dapat melanjutkan ke dokumentasi berikutnya:

**Konfigurasi dan Penggunaan LaTeX Workshop**

Pada bagian tersebut akan dijelaskan lebih rinci mengenai:

- Struktur konfigurasi `settings.json`.
- Compiler dan recipe `latexmk`.
- Automatic Build.
- PDF Viewer dan SyncTeX.
- Clean Auxiliary Files.
- Penggunaan konfigurasi workspace pada proyek penulisan skripsi.