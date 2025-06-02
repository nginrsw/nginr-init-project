# Panduan Pembuatan Proyek Dasar

Panduan ini menjelaskan langkah-langkah untuk membuat struktur dasar sebuah proyek.

## 1. Struktur Direktori

```
myproject/
├── requirements.txt
├── docs/
│   └── *.md
├── src/
│   ├── __init__.py
│   └── main.xr
└── tests/
    └── test_*.xr
```

* **requirements.txt**: Daftar dependensi yang dibutuhkan oleh proyek.
* **docs/**: Folder untuk dokumentasi proyek (format Markdown).
* **src/**: Folder berisi kode sumber utama.

  * `__init__.py`: Menandai folder sebagai package Python.
  * `main.xr`: File utama yang berisi fungsi utama program.
* **tests/**: Folder untuk file-file pengujian.

## 2. Membuat Proyek Baru

1. **Buat struktur folder** seperti contoh di atas.
2. **Buat file `requirements.txt`** untuk mencatat dependensi (misalnya: `math`, `time`, `random`, `os`, `sys`, atau dependensi lain yang dibutuhkan).
3. **Buat file `main.xr`** di dalam folder `src/` sebagai titik masuk utama program.
4. **Buat file pengujian** di dalam folder `tests/` (misalnya: `test_*.xr`).
5. **Jalankan proyek** menggunakan perintah atau *task* yang sesuai (misalnya: task `nginr`).

## 3. Menjalankan Proyek

* Pastikan semua dependensi sudah terpasang.
* Jalankan file utama (`main.xr`) menggunakan preprocessor `nginr` atau task yang sudah disediakan (khusus untuk pengguna VS Code).

## 4. Tips

* Pisahkan kode utama dan kode pengujian dalam folder yang berbeda.
* Gunakan folder `docs/` untuk menyimpan dokumentasi tambahan.
* Simpan daftar dependensi di `requirements.txt` agar instalasi ulang lebih mudah.

## 5. Konfigurasi VS Code: Setting dan Task

### a. Setting Sintaks

Agar file `.xr` dikenali sebagai Python (untuk highlight sintaks dan integrasi alat bantu lain), tambahkan konfigurasi berikut ke `settings.json`.

Cara Membuka `settings.json` (User Settings):

* Buka VS Code.
* Klik menu **File → Preferences → Settings** (atau tekan `Ctrl + ,`).
* Di pojok kanan atas panel Settings, klik ikon `{}` (Open Settings (JSON)).
* Tambahkan kode berikut ke dalam JSON:

```json
"files.associations": {
  "*.xr": "python"
}
```

> Jika sudah ada bagian `files.associations`, kamu cukup menambahkan baris `"*.xr": "python"` di dalamnya.

### b. Menonaktifkan Ekstensi Python (Direkomendasikan)

Untuk menghindari peringatan error dari linter Python (seperti `fn` yang bukan keyword Python), **disarankan untuk menonaktifkan ekstensi Python** sepenuhnya pada proyek `.xr`.

#### Langkah-langkah:

1. Buka **Command Palette** (`Ctrl+Shift+P`).
2. Ketik dan pilih: `Extensions: Disable (Workspace)`
3. Cari **Python** lalu pilih untuk menonaktifkan.
4. VS Code akan menawarkan untuk **menonaktifkan ekstensi lain yang terhubung dengan Python** (seperti Jupyter, Pylance, dll) — **pilih "Yes" atau "Disable All"** agar tidak ada linter aktif yang mengganggu.

> Jangan khawatir, ini hanya berlaku untuk proyek ini saja (workspace). Ekstensi Python tetap aktif untuk proyek lain.

### c. Task untuk Menjalankan File

Buat file `tasks.json` di dalam folder `.vscode/` dengan isi seperti berikut:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // Ganti PATH/TO sesuai lokasi nginr Anda
      "args": [
        "${file}"
      ],
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

* Pastikan path pada `command` sesuai dengan lokasi `nginr` di sistem Anda.
* Gunakan `${HOME}` agar lebih portabel.
* Simpan file ini sebagai `.vscode/tasks.json` di root proyek.

### d. Catatan untuk Pengguna Ekstensi ErrorLens

Jika Anda menggunakan ekstensi **ErrorLens**, perhatikan bahwa **ErrorLens akan tetap memunculkan peringatan jika ada linter aktif** seperti Python/Pylance. Maka dari itu:

* **Matikan ekstensi Python seperti dijelaskan di atas**.
* Alternatif lain: **nonaktifkan ErrorLens sementara** jika masih mengganggu.
