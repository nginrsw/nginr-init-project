# Panduan Pembuatan Project Dasar

Panduan ini menjelaskan langkah-langkah membuat project dasar seperti struktur `project`.

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

- **requirements.txt**: Daftar dependensi yang dibutuhkan project.
- **docs/**: Dokumentasi project (format markdown).
- **src/**: Kode sumber utama project.
    - `__init__.py`: Menandakan folder sebagai package Python.
    - `main.xr`: File utama yang berisi fungsi utama program.
- **tests/**: Folder untuk file-file pengujian.

## 2. Membuat Project Baru
1. **Buat struktur folder** seperti di atas.
2. **Buat file `requirements.txt`** untuk mencatat dependensi (misal: `math`, `time`, `random`, `os`, `sys` atau apapun diperlukan).

4. **Buat file pengujian** di folder `tests/` (misal: `test_*.xr`).
5. **Jalankan project** menggunakan perintah atau task yang sesuai (misal: task `nginr`).

## 3. Menjalankan Project
- Pastikan dependensi sudah terpasang.
- Jalankan file utama (`main.xr`) menggunakan nginr preprocessor atau task yang sudah disediakan dibawah (khusus vscode).

## 4. Tips
- Selalu pisahkan kode utama dan kode pengujian.
- Gunakan folder `docs/` untuk dokumentasi tambahan.
- Simpan dependensi di `requirements.txt` agar mudah diinstal ulang.

## 5. Contoh Konfigurasi Task VS Code
Untuk menjalankan file `.xr` dengan task di VS Code, buat file `tasks.json` di folder `.vscode/` dengan isi seperti berikut:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // ganti path sesuai lokasi nginr terinstall
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

- Pastikan path pada bagian `command` sudah sesuai dengan lokasi `nginr` di sistem Anda. Gunakan `${HOME}` untuk path home agar lebih portabel.
- Simpan file ini sebagai `.vscode/tasks.json` di root project.
- jika menggunakan `errorlens` extension, pastikan python interpreter `tidak di-set ke versi apapun` agar `errorlens` tidak memberikan warning terus menerus ke line yg memiliki deklarasi `fn`, kenapa? karna kita tidak langsung menggunakan `interpreter python` langsung, melainkan menggunakan `preprocessor nginr`.