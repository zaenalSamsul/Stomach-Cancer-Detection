# Image Processing untuk Deteksi Kanker Lambung

Skrip ini melakukan beberapa langkah pemrosesan citra untuk menganalisis dan melakukan segmentasi gambar guna mendeteksi kemungkinan kanker lambung. Langkah-langkahnya meliputi menampilkan gambar asli, membaginya menjadi superpiksel, dan menerapkan berbagai metode segmentasi.

## Langkah-langkah

### 1. Menampilkan Gambar Asli
- **Deskripsi:**
  Gambar asli dimuat menggunakan pustaka OpenCV (`cv2`) dan dikonversi ke format RGB untuk memastikan warna ditampilkan dengan benar dalam analisis dan visualisasi.
- **Output:**
  Gambar asli ditampilkan menggunakan Matplotlib.

### 2. Pembagian Gambar (Superpiksel SLIC)
- **Deskripsi:**
  Gambar dibagi menjadi beberapa segmen kecil yang disebut superpiksel menggunakan algoritma **SLIC (Simple Linear Iterative Clustering)**. Superpiksel membantu menyederhanakan proses analisis gambar dengan mengelompokkan piksel berdasarkan kemiripan fitur.
- **Fungsi Utama:**
  `slic` dari pustaka `skimage.segmentation`.
- **Output:**
  Gambar dengan batas superpiksel ditampilkan menggunakan fungsi `mark_boundaries`.

### 3. Metode Segmentasi

#### 3.1 Statistical Region Merging (SRM)
- **Deskripsi:**
  Metode ini menggunakan properti statistik dari intensitas piksel untuk membentuk wilayah-wilayah yang serupa. Ambang batas ditentukan berdasarkan nilai rata-rata intensitas gambar grayscale.
- **Fungsi Utama:**
  - `rgb2gray` untuk mengubah gambar ke grayscale.
  - `label` untuk memberi label pada wilayah dengan nilai di atas ambang.
- **Output:**
  Batas wilayah segmentasi ditampilkan pada gambar asli.

#### 3.2 Region Growing (RG)
- **Deskripsi:**
  Metode ini memulai segmentasi dari titik awal (seed point) dan memperluas wilayah berdasarkan kesamaan piksel (misalnya, intensitas). Flood-fill digunakan untuk memperluas wilayah secara iteratif.
- **Langkah Utama:**
  1. Gambar diubah ke grayscale.
  2. Mask biner dibuat menggunakan ambang berdasarkan rata-rata intensitas.
  3. Algoritma flood-fill diterapkan dari titik tengah gambar.
- **Fungsi Utama:**
  `cv2.floodFill`.
- **Output:**
  Wilayah yang diperluas oleh algoritma ditampilkan sebagai area yang terisi.

#### 3.3 Simplified Region Merging with Weighted Region Growing (SRMWRG)
- **Deskripsi:**
  Metode ini menggunakan deteksi tepi untuk menyederhanakan proses segmentasi. Tepi objek dalam gambar diidentifikasi menggunakan algoritma Canny.
- **Fungsi Utama:**
  `cv2.Canny` untuk mendeteksi tepi.
- **Output:**
  Peta tepi yang menyoroti batas objek dalam gambar.

### 4. Menyimpan Hasil
- **Deskripsi:**
  Hasil dari setiap metode segmentasi disimpan sebagai file gambar untuk analisis lebih lanjut. Lokasi penyimpanan file telah ditentukan dalam skrip:
  - Gambar tersegmentasi: `/content/partitioned_image.jpg`
  - Gambar hasil SRM: `/content/srm_segmented.jpg`
  - Gambar hasil RG: `/content/rg_segmented.jpg`
  - Gambar hasil SRMWRG: `/content/srmwrg_segmented.jpg`

## Penjelasan Hasil

### **1. Gambar Tersegmentasi (Statistical Region Merging - SRM)**
- **Deskripsi:**
  Metode SRM digunakan untuk membagi gambar ke dalam wilayah-wilayah berdasarkan kesamaan statistik intensitas piksel.
- **Hasil:**
  - Wilayah yang disorot dengan batas kuning menunjukkan area yang dianggap serupa secara statistik.
  - Wilayah ini mencakup area yang menonjol pada gambar, seperti tumor atau struktur abnormal lainnya.
- **Analisis:**
  - Metode ini efektif dalam membedakan antara area utama (tumor) dan latar belakang.
  - Akurasi segmentasi bergantung pada ambang batas yang ditentukan dari intensitas rata-rata gambar grayscale.

### **2. Gambar Tersegmentasi (Region Growing - RG)**
- **Deskripsi:**
  Metode Region Growing diterapkan untuk memperluas wilayah dari titik awal (seed point) berdasarkan kesamaan piksel.
- **Hasil:**
  - Wilayah terang di tengah gambar menunjukkan area yang berhasil diperluas oleh algoritma. Area ini mencakup kemungkinan lokasi tumor.
  - Latar belakang yang gelap membantu memperjelas kontras dengan area target.
- **Analisis:**
  - Algoritma ini berguna untuk mendeteksi wilayah dengan perbedaan intensitas yang jelas.
  - Keberhasilan segmentasi sangat bergantung pada pemilihan seed point dan nilai ambang.

### **3. Gambar Tersegmentasi (SRMWRG)**
- **Deskripsi:**
  Metode SRMWRG menggunakan algoritma Canny untuk mendeteksi tepi objek dalam gambar.
- **Hasil:**
  - Tepi objek yang terdeteksi membantu memperjelas batas wilayah yang mencurigakan.
  - Batas yang terlihat dapat digunakan untuk analisis lebih lanjut.
- **Analisis:**
  - Pendekatan ini efektif dalam membedakan batas area abnormal (misalnya, tumor) dari latar belakang.
  - Hasil segmentasi sangat bergantung pada parameter deteksi tepi seperti ambang atas dan bawah.

## Penggunaan
Untuk menjalankan skrip ini, pastikan pustaka berikut sudah terinstal:
- OpenCV (`cv2`)
- NumPy
- Scikit-Image
- Matplotlib

Eksekusi skrip di lingkungan Python yang mendukung pustaka tersebut. Ganti variabel `image_path` dengan jalur ke gambar input Anda.

