# 🚀 Modul Praktikum 2  
## Batch Data Ingestion & Processing with Spark (Enterprise Edition)

Repositori ini berisi implementasi pipeline data berbasis **Apache Spark (PySpark)** untuk memproses data transaksi harian e-commerce dalam skenario **Batch Processing**.

Proyek ini merupakan bagian dari Praktikum **Big Data Technology**  
Program Studi Teknologi Informasi – UIN Antasari.

---

## 📌 Deskripsi Proyek

Proyek ini mensimulasikan pemrosesan data dalam volume besar yang tidak membutuhkan respons real-time (Batch Processing).

Data mentah:
1. Dibersihkan (Data Cleaning)
2. Ditransformasikan
3. Dihitung metrik bisnisnya
4. Disimpan ke dalam Data Lake

Arsitektur penyimpanan menggunakan pendekatan **Medallion Architecture (Raw → Clean → Curated)** sehingga data siap digunakan untuk Business Intelligence (BI) dan analitik lanjutan.

---

## 🛠️ Environment & Teknologi

- **Bahasa Pemrograman**: Python 3
- **Engine Pemrosesan Data**: Apache Spark (PySpark)
- **Sistem Operasi**: Linux Environment (WSL - Ubuntu)
- **Code Editor**: Visual Studio Code + Remote WSL Extension
- **Format Penyimpanan**: Parquet (Columnar Storage)

---

## 📂 Struktur Direktori

Struktur proyek mengikuti standar Data Lake berlapis (Medallion Architecture):

```text
bigdata-project/
├── data/
│   ├── raw/        # Data mentah (CSV)
│   ├── clean/      # Data tervalidasi (Parquet)
│   └── curated/    # Data siap analitik (Parquet)
├── logs/           # Log eksekusi pipeline
└── scripts/
    └── batch_pipeline_enterprise.py
```

---

## ⚙️ Setup & Instalasi

### 1️⃣ Persiapan WSL & Dependensi

Pastikan WSL (Ubuntu) sudah terinstal:

```bash
wsl --install
```

Update sistem dan instal Java 17 (Spark berjalan di atas JVM):

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

Instal Python dan Virtual Environment:

```bash
sudo apt install python3-full python3-venv python3-pip -y
```

---

### 2️⃣ Integrasi VS Code

- Install extension **WSL**
- Install extension **Python**
- Buka proyek melalui:
  
  ```
  WSL: New Window → Open Folder
  ```

- Aktifkan virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
pip install pyspark
```

---

### 3️⃣ Persiapan Dataset

Letakkan file berikut ke dalam folder:

```
data/raw/ecommerce_raw.csv
```

---

## 🚀 Cara Menjalankan Pipeline

1. Buka terminal di VS Code (mode WSL).
2. Aktifkan virtual environment:

```bash
source venv/bin/activate
```

3. Jalankan pipeline:

```bash
python scripts/batch_pipeline_enterprise.py
```

4. Jika berhasil, folder berikut akan terisi:

- `data/clean/`
- `data/curated/`

Semua data tersimpan dalam format **Parquet** dan sudah dipartisi.

---

## 🧠 Konsep yang Diimplementasikan

### ✅ Explicit Schema
Menggunakan schema eksplisit untuk:
- Menghindari kesalahan tipe data
- Performa lebih cepat dibanding `inferSchema`

### ✅ Data Cleaning & Validation
- Menghapus duplikasi
- Menghapus nilai null
- Menyaring harga & kuantitas > 0
- Validasi format tanggal

### ✅ Business Aggregation
Menghasilkan metrik:
- Total Revenue per Category
- Top 5 Produk berdasarkan kuantitas
- Average Transaction Value per Customer

### ✅ Partition Strategy (Partition Pruning)
Data dipartisi berdasarkan kolom `category` untuk:
- Mempercepat query
- Mengurangi I/O
- Optimasi performa analitik

### ✅ Storage Optimization
Menggunakan **Parquet (Columnar Format)** yang:
- Lebih kecil ukuran filenya
- Lebih cepat untuk query agregasi
- Mendukung predicate pushdown

---

## 📊 Output Pipeline

Layer yang dihasilkan:

| Layer    | Format   | Kegunaan |
|----------|----------|----------|
| Raw      | CSV      | Data mentah |
| Clean    | Parquet  | Data tervalidasi |
| Curated  | Parquet  | Data siap BI & Analytics |

---

## 📈 Use Case

Pipeline ini dapat dikembangkan lebih lanjut untuk:

- Integrasi dengan Apache Airflow
- Deployment ke AWS S3 / GCP
- Integrasi dengan Power BI / Tableau
- Implementasi Data Quality Framework
- Real Enterprise Data Engineering Project

---

## 👨‍💻 Author

Muhammad Raihan Azmi  
Praktikum Big Data Technology – 2026  
Program Studi Teknologi Informasi  
UIN Antasari

---
