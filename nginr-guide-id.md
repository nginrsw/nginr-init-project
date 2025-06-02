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

**Cara membuka `settings.json` (User Settings):**

1. Buka VS Code.
2. Klik menu **File → Preferences → Settings** (atau tekan `Ctrl + ,`).
3. Di pojok kanan atas panel Settings, klik ikon `{}` (Open Settings (JSON)).
4. Tambahkan kode berikut ke dalam JSON:

```json
"files.associations": {
  "*.xr": "python"
}
```

> Jika sudah ada bagian `files.associations`, kamu cukup menambahkan baris `"*.xr": "python"` di dalamnya.

---

### b. Menonaktifkan Ekstensi Python (Direkomendasikan)

Untuk menghindari peringatan atau error sintaks dari linter Python (misalnya `fn` dianggap salah karena bukan keyword Python standar), **disarankan untuk menonaktifkan ekstensi Python khusus untuk proyek ini**.

#### Cara menonaktifkan ekstensi Python hanya untuk satu proyek (workspace):

1. Buka **sidebar Extensions** (klik ikon kotak atau tekan `Ctrl+Shift+X`).

2. Ketik **Python** di kotak pencarian.

3. Temukan ekstensi **Python** (biasanya oleh Microsoft).

4. Klik ikon roda gigi **⚙️** di sebelah ekstensi, lalu pilih:

   > **"Disable (Workspace)"**

5. Jika muncul pertanyaan seperti:

   > *"This extension depends on other extensions. Do you want to disable them too?"*

   Pilih **"Yes" atau "Disable All"**.

Ini akan otomatis menonaktifkan ekstensi tambahan seperti:

* **Pylance**
* **Jupyter**
* **Python Debugger**, dll.

> Ini hanya berlaku untuk folder proyek ini saja. Di proyek lain, ekstensi Python tetap aktif seperti biasa.

---

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

---

### d. Catatan untuk Pengguna Ekstensi ErrorLens

Jika Anda menggunakan ekstensi **ErrorLens**, perlu diketahui bahwa ErrorLens hanya menampilkan pesan dari ekstensi lain (seperti Python atau Pylance). Oleh karena itu:

* **Disarankan untuk menonaktifkan ekstensi Python**, agar pesan error tidak muncul terus.
* Jika ErrorLens masih terlalu mengganggu, kamu bisa **menonaktifkannya sementara** lewat ikon roda gigi di sidebar Extensions.
