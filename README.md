# 🏦 Customer Segmentation – Bank ABC

## 📌 Project Overview

Dalam proyek ini, dilakukan segmentasi pelanggan (customer segmentation) berdasarkan data penggunaan kartu kredit nasabah selama 6 bulan terakhir. Segmentasi ini bertujuan untuk membantu tim marketing Bank ABC dalam memahami perilaku nasabah dan merancang strategi pemasaran yang lebih efektif dan personal.

Proses segmentasi dilakukan menggunakan pendekatan unsupervised learning, tepatnya **K-Means Clustering**, dengan terlebih dahulu melakukan reduksi dimensi menggunakan **Principal Component Analysis (PCA)**.

---

## 🎯 Business Objectives

1. Mengelompokkan nasabah berdasarkan pola penggunaan kartu kredit mereka.
2. Memberikan **rekomendasi bisnis spesifik** untuk tiap klaster yang terbentuk.
3. Menjawab pertanyaan analisis eksploratori berikut:
   - Apakah terdapat pola hubungan antara **TENURE** dengan variabel **PURCHASES**, **BALANCE**, dan **PAYMENTS**?
   - Apakah nasabah dengan **CREDIT_LIMIT** tinggi lebih sering melakukan pembelian (**PURCHASES_FREQUENCY**)?

---

## 🗃️ Dataset Summary

Dataset berisi informasi penggunaan kartu kredit nasabah selama 6 bulan terakhir, mencakup:
- Aktivitas pembelanjaan (ONEOFF_PURCHASES, INSTALLMENTS_PURCHASES)
- Frekuensi transaksi (PURCHASES_FREQUENCY)
- Saldo kartu (BALANCE)
- Limit kredit (CREDIT_LIMIT)
- Pembayaran dan tagihan (PAYMENTS, MINIMUM_PAYMENTS)
- Lama kepemilikan kartu (TENURE)
- Fitur tunai (CASH_ADVANCE)

---

## 📊 Exploratory Data Analysis (EDA)

### 🔹 TENURE vs PURCHASES, BALANCE, PAYMENTS

Terdapat pola bahwa semakin lama nasabah memiliki kartu (TENURE), cenderung:
- Memiliki saldo yang lebih tinggi
- Melakukan lebih banyak transaksi pembelian
- Membayar lebih banyak tagihan

📌 **Rekomendasi**:
Target nasabah dengan TENURE tinggi sebagai segmen potensial untuk program loyalitas dan penawaran eksklusif.

---

### 🔹 CREDIT_LIMIT vs PURCHASES_FREQUENCY

Ditemukan korelasi positif antara **CREDIT_LIMIT** dan **PURCHASES_FREQUENCY**. Nasabah dengan limit yang lebih tinggi cenderung bertransaksi lebih sering.

📌 **Rekomendasi**:
Berikan peningkatan limit kredit secara selektif kepada nasabah aktif agar semakin sering bertransaksi, namun tetap dikontrol dengan credit scoring internal.

---

## ⚙️ Dimensionality Reduction with PCA

Dataset awal memiliki banyak fitur yang saling berkorelasi. Oleh karena itu dilakukan reduksi dimensi menggunakan PCA:

- PCA mempertahankan **95% informasi** dari dataset asli dengan hanya **10 komponen utama**.
- Hal ini membuat model clustering lebih efisien tanpa kehilangan informasi penting.

---

## 🔍 Clustering with K-Means

Dilakukan pemilihan jumlah cluster optimal menggunakan dua metode:
- **Elbow Method** menunjukkan potensi terbaik pada `k=4`
- **Silhouette Score** menunjukkan hasil terbaik pada `k=3`

📌 **Keputusan Akhir**: Menggunakan **3 cluster**, karena memberikan pembagian yang lebih seimbang dan interpretatif secara bisnis.

---

## 📈 Cluster Interpretation & Business Recommendations

### ✅ Cluster 0 – Nasabah Aktif Belanja
- Saldo dan limit tertinggi
- Frekuensi belanja maksimal
- Pembayaran besar, tapi tidak lunas penuh
- Tidak menggunakan cash advance

📌 **Rekomendasi**:
- Berikan program reward dan cashback
- Dorong pelunasan penuh tagihan
- Pertahankan loyalitas dengan program eksklusif

---

### 💸 Cluster 1 – Minim Transaksi, Sering Tarik Tunai
- Pembelian sangat rendah
- Cash advance tinggi
- Limit dan saldo sedang
- Tidak pernah membayar penuh

📌 **Rekomendasi**:
- Edukasi risiko penggunaan cash advance
- Tawarkan promo belanja untuk dorong perubahan perilaku
- Monitoring ketat terhadap pembayaran

---

### 🧾 Cluster 2 – Stabil dan Bertanggung Jawab
- Saldo dan limit terendah
- Cicilan pembelian aktif
- Tidak tarik tunai
- Frekuensi transaksi sedang
- Paling sering membayar tagihan secara penuh

📌 **Rekomendasi**:
- Tawarkan bunga cicilan rendah
- Naikkan limit secara bertahap
- Sediakan pengingat pembayaran otomatis

---

## 📦 Model Output

- Model akhir menggunakan **PCA + KMeans**
- Jumlah cluster: **3**
- Model disimpan menggunakan `joblib` untuk inference ke data baru

---

## 🧪 Model Inference

Model diuji pada data baru (yang belum diskalakan), dan mampu memberikan prediksi klaster dengan baik setelah dilakukan preprocessing (scaling + PCA).

---

## 📌 Final Conclusion

- Segmentasi nasabah berhasil dilakukan dengan 3 klaster utama yang memiliki karakter unik.
- Setiap klaster diberikan **rekomendasi bisnis** yang spesifik dan actionable.
- Ditemukan insight penting dari EDA, khususnya terkait pengaruh TENURE dan CREDIT_LIMIT terhadap perilaku nasabah.

---

## 🧠 Tech Stack

- Python
- Scikit-learn
- Pandas, NumPy
- Seaborn, Matplotlib
- Jupyter Notebook
- Google BigQuery (SQL)

---

## 📁 File Structure
📦 customer_segmentation_project/
│
├── 📄 README.md
├── 📓 P1G6_Set_1.ipynb
├── 📂 data/
│   └── credit_card_data.csv
├── 📂 models/
│   ├── kmeans_model.pkl
│   ├── scaler.pkl
│   └── pca.pkl
