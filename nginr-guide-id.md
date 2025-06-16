# Panduan Setup Proyek Dasar

Panduan ini menjelaskan langkah-langkah untuk membuat struktur proyek dasar.

## 1. Struktur Direktori

```plaintext
project_name/
├── README.md
├── requirements.txt
├── nginr_config.yaml
├── docs/
│   ├── architecture.md
│   ├── api.md
│   └── dev-notes.md
├── src/
│   ├── __init__.py  # Kode sumber utama (file nginr)
│   └── main.xr
├── tests/
│   └── test_main.xr # Tes untuk main.xr
└── .gitignore
```

* **requirements.txt**: File teks yang berisi daftar dependensi Python yang dibutuhkan proyek. Memudahkan pemasangan semua paket yang diperlukan menggunakan alat seperti `pip`.

* **docs/**: Direktori yang berisi dokumentasi tambahan proyek dalam format Markdown (`.md`), seperti:

  * `architecture.md`: Menjelaskan arsitektur keseluruhan proyek.
  * `api.md`: Dokumentasi API, jika ada.
  * `dev-notes.md`: Catatan pengembang dan informasi penting untuk kontributor.

* **src/**: Folder yang berisi file kode sumber utama dengan ekstensi `.xr`, ditulis menggunakan sintaks `nginr`.

  * `main.xr`: File kode sumber utama yang berisi logika inti aplikasi.

  > **Catatan:** Folder ini tidak berisi `__init__.py` karena bukan paket Python, melainkan folder untuk skrip dengan sintaks khusus.

* **tests/**: Direktori untuk file-file tes yang memverifikasi kebenaran kode sumber di `src/`.

  * `test_main.xr`: Skrip tes yang dibuat untuk menguji fungsi-fungsi di `main.xr`.

## 2. Membuat Proyek Baru

Nginr juga dapat membantu Anda membuat struktur proyek baru dengan cepat. Gunakan perintah init:

```
nginr init your_project_name
```

Dan Anda akan mendapatkan struktur proyek seperti yang ditunjukkan di atas.

## 3. Menjalankan Proyek

* Pastikan semua dependensi sudah terpasang.
* Jalankan file utama (`main.xr`) menggunakan preprocessor `nginr` atau task yang sudah didefinisikan (terutama jika menggunakan VS Code).

## 4. Tips

* Pisahkan kode utama dan kode tes ke dalam folder yang berbeda.
* Gunakan folder `docs/` untuk dokumentasi tambahan apa pun.
* Simpan daftar dependensi di `requirements.txt` agar mudah diinstal ulang.

## 5. Konfigurasi VS Code: Pengaturan dan Task

### a. Syntax Highlighting

Agar file `.xr` dikenali sebagai file Python (untuk syntax highlighting dan integrasi dengan tools lain), tambahkan konfigurasi berikut ke `settings.json` Anda.

**Cara membuka `settings.json` (Pengaturan Pengguna):**

1. Buka VS Code.
2. Pergi ke **File → Preferences → Settings** (atau tekan `Ctrl + ,`).
3. Di pojok kanan atas panel Settings, klik ikon `{}` (Open Settings (JSON)).
4. Tambahkan ini ke dalam JSON:

```json
"files.associations": {
  "*.xr": "python"
}
```

> Jika bagian `files.associations` sudah ada, tambahkan `"*.xr": "python"` di dalamnya.

---

### b. Menonaktifkan Ekstensi Python (Direkomendasikan)

Untuk menghindari error atau peringatan dari linter Python (misal `fn` dianggap bukan keyword Python standar), **disarankan menonaktifkan ekstensi Python hanya untuk proyek ini saja**.

#### Cara menonaktifkan ekstensi Python untuk workspace/proyek tertentu:

1. Buka **Extensions sidebar** (klik ikon kotak atau tekan `Ctrl+Shift+X`).

2. Cari ekstensi **Python** di kolom pencarian.

3. Temukan ekstensi **Python** (biasanya dari Microsoft).

4. Klik ikon **⚙️ gear** di sebelah ekstensi, lalu pilih:

   > **"Disable (Workspace)"**

5. Jika muncul notifikasi seperti:

   > *"Ekstensi ini bergantung pada ekstensi lain. Apakah Anda ingin menonaktifkan semuanya?"*

   Pilih **"Yes"** atau **"Disable All"**.

💡 Ini akan secara otomatis menonaktifkan ekstensi tambahan seperti:

* **Pylance**
* **Jupyter**
* **Python Debugger**, dan lainnya.

> Jika ingin menggunakan Python lagi, jangan lupa untuk mengaktifkan kembali ekstensi yang dinonaktifkan agar linting dan fungsi lainnya dapat berjalan kembali.
> 
> Atau bisa menggunakan extensi vscode yg saya buat bernama [nginr-support](https://github.com/nginrsw/nginr-support), baca dan pahami baik-baik cara mengatur dan menggunakannya.

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
      "command": "${HOME}/PATH/TO/nginr", // Ganti PATH/TO dengan lokasi nginr Anda
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

* Pastikan path pada `command` mengarah ke lokasi nginr yang benar di sistem Anda.
* Gunakan `${HOME}` agar lebih portabel.
* Simpan file ini sebagai `.vscode/tasks.json` di root proyek Anda.

---

### d. Catatan untuk Pengguna Ekstensi ErrorLens

Jika Anda menggunakan ekstensi **ErrorLens**, perlu diketahui bahwa ekstensi ini hanya menampilkan pesan dari ekstensi lain (seperti Python atau Pylance). Oleh karena itu:

* **Disarankan menonaktifkan ekstensi Python** seperti yang dijelaskan di atas agar pesan error tidak terus muncul.
* Jika ErrorLens masih terlalu mengganggu, Anda bisa **menonaktifkannya sementara** lewat ikon gear di Extensions sidebar.
