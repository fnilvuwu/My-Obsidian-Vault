---
created: 2025-04-23T23:06
updated: 2025-04-23T23:17
---
### 🔍 Jenis-Jenis Analitik:

1. **Descriptive Analytics**
    - Fokus pada pemahaman **apa yang telah terjadi**.
2. **Diagnostic Analytics**
    - Menganalisis **penyebab** dari suatu kejadian atau masalah.
3. **Predictive Analytics**
    - Meramalkan **apa yang mungkin terjadi** di masa depan.
4. **Prescriptive Analytics**
    - Memberikan **rekomendasi tindakan** berdasarkan hasil analisis deskriptif & prediktif.
5. **Cognitive Analytics**
    - Menggabungkan **AI, machine learning, NLP** untuk memahami **data tidak terstruktur** seperti teks, gambar, video.

---

### 📦 10 V dari Big Data:

- Volume, Velocity, Variety, Veracity, Value, Validity, Variability, Venue, Vocabulary, Vagueness

---

### 📂 Jenis-Jenis Data:

- **Structured**: API, Tabel, Database
- **Semi-structured**: JSON, XML, CSV, NoSQL, Excel
- **Unstructured**: Gambar, Video, Audio, PDF

---

### 💡 Definisi Big Data:

Big data adalah ilmu mengolah data yang **bervolume besar** dan **tidak dapat diolah** dengan teknik konvensional.

---

### 🔁 Siklus Analisis Big Data:

#### Komponen Spark:

- **Spark Core**: Mesin utama untuk pemrosesan paralel dan terdistribusi.
- **Spark SQL**: Library untuk pemrosesan data relasional.
- **MLLib**: Library algoritma machine learning.
- **GraphX**: Library untuk komputasi grafik.
- **Spark Streaming**: Untuk pemrosesan data **real-time**.

#### Preprocessing:

- Data Integration
- Data Imputation
- Categorical Encoding / One-hot Encoding
- Scaling / Normalization
- Outlier Detection

---

### ☁️ Cloud Computing:

Teknologi untuk **menyewa sumber daya komputasi** tanpa perlu memiliki server fisik.

---

### 🏗️ Arsitektur / Platform Big Data:

1. Data Sources
2. Data Ingestion
3. Data Storage
4. Data Processing
5. Data Analysis
6. Data Visualization

---

### 🐘 Arsitektur Hadoop:

- **HDFS**: Sistem file terdistribusi.
    - NameNode: Mengelola metadata.
    - DataNode: Menyimpan file/data.
- **YARN**: Platform manajemen resource (scheduling & resource management).
- **MapReduce**: Algoritma pemrosesan data secara terdistribusi.

---

### ⚡ Arsitektur Spark:

- **Spark Driver**: Mengatur eksekusi dan distribusi tugas.
- **Executor**: Menjalankan tugas dari driver.
- **Cluster Manager**: Mengatur sumber daya klaster (misal: YARN, Spark Standalone).

---

### 📥 Teknik Pengambilan Data:

- Web Scraping
- IoT (sensor)
- API
- Streaming Platform (YouTube, Twitter)

---

### 🗃️ Fase MapReduce:

1. **Mapper**: Memetakan input ke dalam (k',v')
2. **Shuffle & Sort**: Kelompokkan berdasarkan kunci, keluaran (k, [v])
3. **Reducer**: Gabungkan nilai dengan kunci yang sama dari berbagai mapper
4. **Combiner (Opsional)**: Menggabungkan output mapper sebelum shuffle

---

### 📈 Data Mining:

Proses menemukan pola dari dataset besar menggunakan metode statistik dan machine learning.

### 🤖 Machine Learning:

Bagian dari AI, memungkinkan komputer belajar dari data untuk membuat prediksi.

#### Jenis:

- **Supervised Learning**
- **Unsupervised Learning**
- **Reinforcement Learning**
- **Self-supervised Learning**
- **Semi-supervised Learning**

---

### 🧠 Metode Data Mining:

- **Klasifikasi**
- **Klastering**
- **Asosiasi**
- **Regresi**

---

### 🔬 Contoh Arsitektur/Platform Big Data

1. **Data Sources**
2. **Data Ingestion**
3. **Data Storage**
4. **Data Processing**
5. **Data Analytics**
6. **Data Visualization**

---

## 🆚 Ringkasan Perbedaan DataFrame vs RDD

### 📐 Struktur Data

- **DataFrame**: Terstruktur (seperti tabel).
- **RDD**: Tidak terstruktur (elemen bebas).

### 🧱 Skema

- **DataFrame**: Skema eksplisit (kolom & tipe data jelas).
- **RDD**: Tidak eksplisit (array/objek).

### ⚡ Efisiensi

- **DataFrame**: Lebih cepat (optimasi Catalyst & Tungsten).
- **RDD**: Lebih lambat (tidak otomatis dioptimasi).

### 🔧 Operasi

- **DataFrame**: SQL & API tinggi (mudah digunakan).
- **RDD**: Low-level (`map()`, `filter()`, `reduce()`).
### ✅ Keuntungan

- **DataFrame**:
    - Mudah dibaca & digunakan.
    - Optimasi otomatis.
    - Support SQL.
        
- **RDD**:
    
    - Fleksibel (semi-struktur/tak terstruktur).
    - Cocok untuk operasi kompleks.

---

### 💥 Perbandingan Spark, Hadoop, dan Flink

| Fitur              | Hadoop                               | Spark                                 |
| ------------------ | ------------------------------------ | ------------------------------------- |
| Model Pemrograman  | MapReduce                            | RDDs (Resilient Distributed Datasets) |
| Kinerja            | Disk-based processing (Hardisk, SSD) | In-memory processing (RAM)            |
| Harga              | Murah                                | Lebih Mahal                           |
| Pemrosesan         | Batch                                | Batch, Streaming                      |
| Bahasa Pemrograman | Java, Pig, Hive                      | Scala, Java, Python, R                |


---