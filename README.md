# Crawling-and-Scrapping-bisnis.com

Proyek ini berfungsi untuk mengambil data artikel dari **Bisnis.com**.  
Tersedia dua mode operasi:  
- **Backtrack** → mengambil artikel berdasarkan rentang tanggal tertentu.  
- **Standard** → mengambil artikel terbaru secara otomatis dalam periode tertentu.  

# Struktur Proyek  
├── crawler.py /Modul scraping
├── backtrack.py /Mode Backtrack (rentang tanggal)
├── standard.py /Mode Standard (ambil terbaru)
├── requirements.txt
└── README.md 

# Gambaran 

## `crawler.py`  
Berisi fungsi inti untuk:
- Mengambil daftar artikel dari halaman (URL dan tanggal terbit).
- Mengambil detail artikel (judul, isi, tanggal terbit).
- Menyimpan hasil ke file JSON.
Fungsi ini dipakai bersama oleh kedua mode (Backtrack dan Standard).

## `backtrack.py`  
Script ini mengakses **crawler.py** untuk mengambil artikel di rentang tanggal tertentu.  
Langkah utama:
- Mengekstrak tanggal dari URL artikel.
- Mengambil daftar URL dari tiap halaman.
- Menyaring dan menyimpan artikel sesuai rentang tanggal.

## `standard.py`  
Script ini mengambil artikel terbaru dalam beberapa hari terakhir secara otomatis.  
Cocok untuk update rutin.  
Langkah utama:
- Mengambil daftar artikel dari halaman utama Bisnis.com.
- Mengecek tanggal terbit artikel.
- Menyimpan artikel terbaru hingga batas tertentu.

# Instalasi
Unduh repo ini atau clone menggunakan Git.
Pasang dependensi:
pip install -r requirements.txt
playwright install

# Cara Menjalankan
## Mode Backtrack
Digunakan untuk mengambil artikel berdasarkan tanggal tertentu.
1. Buka file backtrack.py.
Pada bagian paling bawah, ubah tanggal sesuai kebutuhan:
if __name__ == "__main__":
    asyncio.run(backtrack_crawler("2025-09-19", "2025-09-20"))
2. Jalankan:
python backtrack.py

## Mode Standard
Digunakan untuk mengambil artikel terbaru.
1. Buka file standard.py.
2. Pastikan nilai HARI_TERAKHIR sesuai kebutuhan (default = 3 hari terakhir).
3. Jalankan:
python standard.py

## Contoh Hasil JSON

Hasil scraping disimpan dalam format JSON dengan struktur seperti berikut:

[
  {
    "Link": "https://bisnis.com/read/20250920/...",
    "Judul": "Judul Artikel",
    "Isi_artikel": "Isi artikel lengkap di sini...",
    "Tanggal_terbit": "2025-09-20T10:30:00+07:00"
  },
  {
    "Link": "https://bisnis.com/read/20250920/...",
    "Judul": "Artikel Kedua",
    "Isi_artikel": "Isi artikel lengkap...",
    "Tanggal_terbit": "2025-09-20T09:00:00+07:00"
  }
]

## Arsitektur Proyek

Diagram berikut menunjukkan alur sederhana bagaimana masing-masing file berinteraksi:
flowchart 
    A[backtrack.py (mengambil artikel sesuai tanggal)] --> B[crawler.py (modul scraping inti)]
    D[standard.py (mengambil artikel terbaru)] --> B
    B --> C[File JSON (output hasil scraping)]
