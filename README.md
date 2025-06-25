# 🧠 Penalaran Komputer: Pidana Umum – Kejahatan Terhadap Kesusilaan

Proyek ini mengembangkan sistem **penalaran berbasis kasus (Case-Based Reasoning)** untuk mendukung pencarian dan analisis putusan hukum dalam ranah **Pidana Umum – Kejahatan Terhadap Kesusilaan**. Sistem ini memungkinkan pengguna mencari kasus serupa berdasarkan ringkasan fakta dan mengevaluasi performa retrieval menggunakan metode NLP dan Machine Learning.

---

## ⚙️ Teknologi yang Digunakan

* Python 3.10+
* pandas, scikit-learn
* BeautifulSoup, pdfminer / pdftotext
* Sentence-Transformers (BERT Embedding)
* TF-IDF + SVM
* Google Colab / Jupyter Notebook

---

## 📅 Langkah-Langkah Proyek

### ✅ Tahap 1: Membangun Case Base

* **Seleksi & Unduh Dokumen:** ≥30 putusan, yaitu 40 Data dari Direktori MA RI.
* **Konversi & Ekstraksi Teks:** PDF ➔ teks biasa menggunakan pdfminer atau HTML dengan BeautifulSoup.
* **Pembersihan:** Hapus header, footer, nomor halaman, dan normalisasi teks.
* **Output:** /data/raw/*.txt

### ✅ Tahap 2: Case Representation

* **Ekstraksi Metadata:** Nomor Perkara, Tanggal, Pasal, Pihak, dll.
* **Ekstraksi Konten Kunci:** Ringkasan Fakta dan Argumen Hukum.
* **Feature Engineering:** Panjang teks (jumlah kata), Bag-of-Words (kata kunci), Estimasi QA-pairs.
* **Output:** /data/processed/cases.csv

### ✅ Tahap 3: Case Retrieval

* **Vektorisasi:**

  * TF-IDF menggunakan TfidfVectorizer
  * BERT Embedding menggunakan paraphrase-multilingual-MiniLM-L12-v2
* **Splitting Dataset:** Train/Test dengan rasio 80:20.
* **Model Retrieval:**

  * TF-IDF + SVM
  * BERT Similarity
* **Evaluasi Awal:**

  * Simpan 10 query uji di /data/eval/queries.json

### ✅ Tahap 4: Solution Reuse

* **Ambil Solusi Top-k:** Amar Putusan/Ringkasan.
* **Prediksi Solusi:** Majority Vote / Weighted Similarity.
* **Output:** /data/results/predictions.csv

### ✅ Tahap 5: Evaluasi Model

* **Metrik Evaluasi:** Accuracy, Precision, Recall, F1-score.
* **Visualisasi:**

  * Tabel metrik (retrieval_metrics.csv)
  * Daftar kegagalan (prediction_metrics.csv)

---

## 🚀 Petunjuk Instalasi & Eksekusi

### 1. Clone Repository

bash
git clone https://github.com/tantri17/PENALARAN-KOMPUTER-Pidana-Umum-Kejahatan-Terhadap-kesusilaan.git
cd PENALARAN-KOMPUTER-Pidana-Umum-Kejahatan-Terhadap-kesusilaan
### Note: jika Drive tidak bisa maka dowload pada github bagian "data/Penalaran Komputer3" lalu upload pada drive anda. 


### 2. Install Dependensi

Buat dan jalankan `requirements.txt`:

```bash
pip install -r requirements.txt
```

Isi `requirements.txt`:

```txt
pandas
scikit-learn
beautifulsoup4
pdfminer.six
sentence-transformers
```

Gunakan Google Colab **(disarankan)** atau Jupyter Notebook:

python
!pip install pandas scikit-learn beautifulsoup4 sentence-transformers


### 3. Jalankan End-to-End Pipeline

Buka dan jalankan notebook berikut secara berurutan:

1. `01_cleaning.ipynb` : Konversi dan pembersihan teks putusan.
2. `02_case_representation.ipynb` : Ekstraksi metadata & fitur.
3. `03_retrieval.ipynb` : Vektorisasi dan retrieval.
4. `04_predict.ipynb` : Prediksi solusi kasus baru.
5. `05_evaluation.ipynb` : Evaluasi dan visualisasi hasil.
---

## 📋 Data Prediksi

Tabel berikut menunjukkan hasil prediksi 10 query uji menggunakan dua pendekatan: **TF-IDF + SVM** dan **BERT Embedding**.

| query\_id | query\_text                                | ground\_truth | pred\_svm | pred\_bert | status\_svm | status\_bert |
| --------- | ------------------------------------------ | ------------- | --------- | ---------- | ----------- | ------------ |
| 1         | Ini adalah isi dokumen hukum nomor 87. ... | 87            | 87        | 87         | BENAR       | BENAR        |
| 2         | Ini adalah isi dokumen hukum nomor 23. ... | 23            | 23        | 23         | BENAR       | BENAR        |
| 3         | Ini adalah isi dokumen hukum nomor 98. ... | 98            | 98        | 98         | BENAR       | BENAR        |
| 4         | Ini adalah isi dokumen hukum nomor 64. ... | 64            | 64        | 64         | BENAR       | BENAR        |
| 5         | Ini adalah isi dokumen hukum nomor 16. ... | 16            | 16        | 16         | BENAR       | BENAR        |
| 6         | Ini adalah isi dokumen hukum nomor 34. ... | 34            | 34        | 34         | BENAR       | BENAR        |
| 7         | Ini adalah isi dokumen hukum nomor 14. ... | 14            | 14        | 14         | BENAR       | BENAR        |
| 8         | Ini adalah isi dokumen hukum nomor 70. ... | 70            | 70        | 70         | BENAR       | BENAR        |
| 9         | Ini adalah isi dokumen hukum nomor 1. ...  | 1             | 0         | 1          | SALAH       | BENAR        |
| 10        | Ini adalah isi dokumen hukum nomor 77. ... | 77            | 77        | 77         | BENAR       | BENAR        |

---

### 🎯 Akurasi Model

| Model          | Akurasi |
| -------------- | ------- |
| TF-IDF + SVM   | 90.00%  |
| BERT Embedding | 100.00% |

![image](https://github.com/user-attachments/assets/3be6a7fb-4e27-4613-92d5-e9098d59ac78)

---

---

## 📄 Hasil Akhir

| Model          | Accuracy | Precision | Recall  | F1-Score |
| -------------- | -------- | --------- | ------- | -------- |
| TF-IDF + SVM   | 90.00%   | 81.82%    | 81.82%   | 81.82%  |
| BERT Embedding | 100.00%  | 100.00%   | 100.00% | 100.00%  |

---
![image](https://github.com/user-attachments/assets/5feb1434-93b3-4b6e-b078-eb0bd98ec439)



## 📄 Struktur Folder

/data
  /raw                 # Teks putusan mentah
  /processed           # Dataset setelah ekstraksi & representasi
  /eval                # Dataset evaluasi & metrik
  /results             # Hasil prediksi solusi


---

## 🔧 Catatan Tambahan

* Pastikan seluruh path di notebook sudah disesuaikan dengan Google Drive atau local.
* Proyek ini hanya mencakup domain **Pidana Umum - Kejahatan Terhadap Kesusilaan**.
* Idealnya digunakan untuk pembelajaran, penelitian, atau pembuatan sistem hukum berbasis AI.

---

📄 **Author:** Tantri Romadhoni S.N

📢 Untuk pertanyaan, silakan hubungi melalui GitHub Issue atau email terkait, Terimakasih.
