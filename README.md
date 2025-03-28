# 🏥 Pemrosesan Citra untuk Deteksi Kanker Lambung 🖼️

Skrip ini dirancang untuk membantu analisis dan segmentasi gambar guna mendeteksi kemungkinan kanker lambung. Dengan serangkaian teknik pemrosesan citra, kita dapat menyoroti area yang mencurigakan dalam gambar medis. Yuk, kita jelajahi langkah-langkahnya! 🚀

---

## 🔎 Langkah-langkah Analisis

### 1️⃣ Menampilkan Gambar Asli 🎨
📌 **Apa yang dilakukan?**
- Mengimpor gambar asli dengan pustaka OpenCV (`cv2`).
- Mengubah gambar ke format RGB agar warna ditampilkan dengan benar.

📌 **Hasil yang diharapkan:**
- Gambar asli ditampilkan menggunakan Matplotlib untuk analisis lebih lanjut.

---

### 2️⃣ Pembagian Gambar dengan Superpiksel (SLIC) 🧩
📌 **Apa itu SLIC?**
- **SLIC (Simple Linear Iterative Clustering)** membagi gambar menjadi beberapa segmen kecil yang disebut *superpiksel*. Ini membantu menyederhanakan analisis dengan mengelompokkan piksel berdasarkan kemiripan fitur.

📌 **Bagaimana cara kerjanya?**
- Menggunakan `slic` dari pustaka `skimage.segmentation`.
- Menampilkan batas-batas superpiksel dengan `mark_boundaries`.

📌 **Hasil yang diharapkan:**
- Gambar dengan garis-garis pembatas superpiksel untuk analisis lebih lanjut.

---

## 🛠️ Metode Segmentasi

### 3️⃣.1 Statistical Region Merging (SRM) 📊
📌 **Bagaimana cara kerjanya?**
- Menggunakan properti statistik intensitas piksel untuk membentuk wilayah serupa.
- Menentukan ambang berdasarkan rata-rata intensitas gambar grayscale.

📌 **Hasil yang diharapkan:**
✅ Batas-batas wilayah segmentasi ditampilkan pada gambar asli.

---

### 3️⃣.2 Region Growing (RG) 🌱
📌 **Konsep Dasar:**
- Memulai segmentasi dari titik awal (*seed point*).
- Wilayah diperluas berdasarkan kesamaan piksel.
- Teknik *flood-fill* digunakan untuk memperluas area secara iteratif.

📌 **Langkah-langkah:**
1️⃣ Konversi gambar ke grayscale.
2️⃣ Buat mask biner berdasarkan ambang intensitas.
3️⃣ Terapkan algoritma *flood-fill* dari titik tengah gambar.

📌 **Hasil yang diharapkan:**
✅ Area yang diperluas oleh algoritma muncul sebagai wilayah terang dalam gambar.

---

### 3️⃣.3 SRMWRG (Simplified Region Merging with Weighted Region Growing) 🔍
📌 **Metode Ini Menggunakan:**
- Deteksi tepi dengan algoritma **Canny** untuk menyederhanakan segmentasi.

📌 **Fungsi Utama:**
- `cv2.Canny` untuk mendeteksi tepi dalam gambar.

📌 **Hasil yang diharapkan:**
✅ Peta tepi yang menyoroti batas-batas objek yang mencurigakan.

---

## 💾 Penyimpanan Hasil
Setiap metode segmentasi menyimpan hasilnya dalam file gambar:
✅ **Superpiksel:** `/content/partitioned_image.jpg`
✅ **Hasil SRM:** `/content/srm_segmented.jpg`
✅ **Hasil RG:** `/content/rg_segmented.jpg`
✅ **Hasil SRMWRG:** `/content/srmwrg_segmented.jpg`

---

## 📊 Analisis Hasil

### 🔬 1. Segmentasi dengan SRM
✅ Area yang disorot dengan batas kuning menunjukkan wilayah yang memiliki kesamaan statistik.
✅ Potensi deteksi area tumor atau struktur abnormal meningkat dengan metode ini.

### 🌿 2. Segmentasi dengan Region Growing
✅ Area yang terang menunjukkan lokasi yang berhasil diperluas dari *seed point*.
✅ Berguna untuk mendeteksi wilayah dengan perbedaan intensitas yang jelas.

### 🖼️ 3. Segmentasi dengan SRMWRG
✅ Tepi objek yang terdeteksi membantu memperjelas batas-batas area mencurigakan.
✅ Berguna untuk memisahkan area abnormal dari latar belakang.

---

## ⚙️ Cara Menggunakan Skrip Ini
Untuk menjalankan skrip, pastikan Anda telah menginstal pustaka berikut:
- OpenCV (`cv2`)
- NumPy
- Scikit-Image
- Matplotlib

📌 **Eksekusi skrip ini di Python dan pastikan variabel `image_path` sudah sesuai dengan lokasi gambar input Anda.**

🚀 **Siap menganalisis gambar medis dengan lebih canggih? Selamat mencoba!** 🏥✨

