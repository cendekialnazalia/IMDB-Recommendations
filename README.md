# 📑 Laporan Proyek Akhir Machine Learning Terapan - Cendekia Luthfieta Nazalia
**Title : Sistem Rekomendasi Film Menggunakan Content-Based Filtering**

# Project Overview 
Industri perfilman mengalami perkembangan yang sangat pesat seiring dengan meningkatnya akses masyarakat terhadap platform streaming dan distribusi digital. Dengan ribuan judul film yang tersedia, pengguna sering mengalami kesulitan dalam menemukan film yang sesuai dengan preferensi mereka. Masalah ini menyebabkan kebutuhan akan sistem rekomendasi yang efektif untuk membantu pengguna menemukan film yang relevan dan meningkatkan pengalaman menonton.

Sistem rekomendasi **content-based filtering** adalah salah satu pendekatan yang memanfaatkan fitur-fitur film, seperti genre, pemeran, sutradara, durasi, dan tagline, untuk memberikan rekomendasi berdasarkan kesamaan konten dengan film yang sudah disukai pengguna. Pendekatan ini memungkinkan rekomendasi yang lebih personal dan sesuai dengan preferensi individu dibandingkan metode umum berbasis popularitas.

## Tujuan Proyek
Tujuan dari proyek ini adalah:
1. Membangun sistem rekomendasi film berbasis content-based filtering menggunakan dataset IMDb Top 250 Movies.
2. Melakukan tahapan data preprocessing, feature engineering, dan feature selection untuk memastikan kualitas data yang optimal.
3. Mengimplementasikan algoritma cosine similarity untuk menghitung kesamaan film.
4. Mengevaluasi performa sistem rekomendasi menggunakan metrik standar seperti Precision@K, Recall@K, dan NDCG@K.
5. Memberikan rekomendasi film yang relevan bagi pengguna berdasarkan preferensi film yang telah diketahui.

## Relevansi Masalah
Berdasarkan studi sebelumnya, pengguna cenderung lebih puas dengan sistem rekomendasi yang dapat menyesuaikan preferensi individual, terutama dalam hal genre dan pemeran favorit ([Ricci et al., 2015](https://scholar.google.com/scholar?q=content+based+recommender+systems+ricci+2015)). Dengan meningkatnya jumlah data film, metode content-based filtering menjadi solusi yang efisien untuk memproses data fitur film dan memberikan rekomendasi yang akurat.

## Referensi
1. Ricci, F., Rokach, L., Shapira, B., & Kantor, P. B. (2015). *Recommender Systems Handbook*. Springer.  
2. Lops, P., Gemmis, M. D., & Semeraro, G. (2011). Content-based recommender systems: State of the art and trends. *Recommender Systems Handbook*, 73–105.  
3. IMDb Top 250 Movies Dataset. [Kaggle Dataset](https://www.kaggle.com/datasets/rajugc/imdb-top-250-movies-dataset).  


---

## BUSINESS UNDERSTANDING

### Problem Statements
1. **Sulitnya pengguna menemukan film yang sesuai preferensi:**  
   Pengguna sering kesulitan memilih film karena banyaknya judul yang tersedia di platform streaming. Hal ini membuat pengalaman menonton menjadi kurang personal dan memakan waktu.

2. **Kurangnya rekomendasi personal yang berbasis konten:**  
   Sistem rekomendasi yang ada sering hanya mengandalkan popularitas atau rating global, sehingga tidak memperhatikan preferensi individu berdasarkan genre, pemeran, atau tema film.

3. **Keterbatasan dalam memanfaatkan data fitur film:**  
   Banyak platform belum mengoptimalkan informasi yang tersedia pada film (genre, tagline, sutradara, cast, durasi, budget, dll.) untuk memberikan rekomendasi yang relevan dan akurat.

### Goals
1. **Menyediakan rekomendasi film yang sesuai preferensi pengguna:**  
   Sistem rekomendasi akan memanfaatkan fitur film untuk menemukan film yang mirip dengan film yang disukai pengguna, sehingga mempermudah pemilihan film.

2. **Meningkatkan personalisasi rekomendasi:**  
   Dengan menggunakan content-based filtering, rekomendasi dapat disesuaikan dengan preferensi individu, memperhitungkan genre, pemeran, sutradara, dan fitur lain yang relevan.

3. **Memaksimalkan penggunaan data fitur film:**  
   Proyek ini akan memproses data numerik dan teks dari film, melakukan feature engineering, serta menghitung kesamaan antarfilm untuk memberikan rekomendasi yang akurat.

#### Solution Approach
1. **Content-Based Filtering dengan Cosine Similarity:**  
   - Menghitung kesamaan film berdasarkan fitur numerik dan tekstual (genre, tagline, cast, sutradara, writers, durasi, rating, budget).  
   - Memberikan rekomendasi film yang mirip dengan film yang telah disukai pengguna.

2. **Optimasi dan Evaluasi Rekomendasi:**  
   - Menggunakan feature selection untuk memilih fitur paling relevan.  
   - Mengevaluasi sistem menggunakan metrik Precision@K, Recall@K, dan NDCG@K untuk memastikan kualitas rekomendasi.

---

## DATA UNDERSTANDING 

### Informasi Dataset
Dataset yang digunakan dalam proyek ini adalah **IMDb Top 250 Movies Dataset**, yang dapat diunduh melalui [Kaggle](https://www.kaggle.com/datasets/rajugc/imdb-top-250-movies-dataset). Dataset ini berisi informasi tentang 250 film terbaik versi IMDb, mencakup berbagai fitur yang relevan untuk sistem rekomendasi.  

Dataset ini memiliki **250 baris** (film) dan **12 kolom fitur utama**, yang memberikan informasi numerik maupun teks yang dapat digunakan untuk membangun model content-based filtering. Sebagian besar data sudah bersih tidak terdapat missing value ataupun duplikasi data, namun terdapat format string yang berbeda pada kolom numeric.

Secara umum, dataset memiliki karakteristik sebagai berikut:
- Variabel numerik: rating, year, run_time, budget, box_office, rank  
- Variabel kategorikal / teks: name, genre, certificate, tagline, casts, directors, writers  

### Deskripsi Variabel
Berikut uraian variabel yang tersedia pada dataset:

1. **rank**: Peringkat film berdasarkan skor IMDb.  
2. **name**: Nama film.  
3. **year**: Tahun rilis film.  
4. **rating**: Rating IMDb film (skala 0–10).  
5. **genre**: Genre film (misal Drama, Crime, Action).  
6. **certificate**: Sertifikasi usia film (misal PG-13, R, Not Rated).  
7. **run_time**: Durasi total film, biasanya dalam format menit atau jam.  
8. **tagline**: Tagline atau slogan film, berupa teks deskriptif singkat.  
9. **budget**: Anggaran produksi film, dalam berbagai format mata uang dan skala (misal juta atau miliar).  
10. **box_office**: Total pendapatan box office global, dalam berbagai format mata uang dan skala.  
11. **casts**: Daftar pemeran utama film.  
12. **directors**: Nama sutradara film.  
13. **writers**: Penulis naskah film.

### Exploratory Data Analysis (EDA) dan Insight
EDA ini membantu memahami karakteristik dataset dan menentukan strategi feature engineering serta preprocessing sebelum membangun sistem rekomendasi.

Beberapa langkah EDA yang dilakukan meliputi:

- **Univariate Exploratory Data Analysis - Deskripsi Variabel**  
  data.info() -> Terdapat 250 data dengan 13 colums dan 3 colums tambahan genre yang sudah kita olah tadi.
  data.describe() -> memahami distribusi awal data, mendeteksi outlier, dan mengetahui rentang nilai dari setiap variabel numerik.
  
- **Exploratory Data Analysis - Rata-rata Ratings berdasarkan Genre**  
  Berdasarkan hasil EDA didapatkan hasil rata-rata rating tertinggi ditempati oleh genre adventure, wastern, action, adventure dan drama.

- **Exploratory Data Analysis - 5 Film Teratas Berdasarkan Rating**  
  Dapat kita lihat the shawshank redemption menempati film teratas berdasarkan rating yaitu 9.3 dan ini juga memvalidasi EDA kita sebelumnya bahwa film drama ada genre dengan rating yang tinggi.

  - **Exploratory Data Analysis - 5 Genre Teratas Berdasarkan Rating**  
  Begitu pula setelah kita lihat 5 genre teratas kita bisa lihat crime dan drama pada posisi teratas

- **Exploratory Data Analysis - 5 Casts Teratas Berdasarkan Rating**  
  Data ini menunjukkan hasil Cast dengan rating tertinggi adalah Scott man, renee blaine, dan kawan-kawan. Ini bisa jadi menunjukkan ketertarikan untuk untuk film dengan cast serupa.
  
- **Exploratory Data Analysis - 5 Directors Teratas Berdasarkan Rating**  
  Data ini menunjukkan hasil Directors dengan rating tertinggi adalah Francis Ford Coppola. Ini bisa jadi menunjukkan ketertarikan untuk untuk film dengan directors serupa.

- **Exploratory Data Analysis - 5 Penulis Teratas Berdasarkan Rating**  
  Data ini menunjukkan hasil Penulis dengan rating tertinggi adalah Stephen King, Frank Darabont. Ini bisa jadi menunjukkan ketertarikan untuk film dengan penulis serupa.

  - **Exploratory Data Analysis - Jumlah Certificate**  
  menampilkan jumlah film per kategori certificate.
Keterangan Certificate Film:
   - **R**           : Sangat tidak untuk anak-anak; banyak kekerasan, seks, dan bahasa kasar.
   - **PG**          : Cukup baik untuk anak-anak; sedikit bahasa atau kekerasan ringan, aman untuk mata kecil.  
   - **PG-13**       : Orangtua disarankan mendampingi remaja; aksi dan ketegangan lebih.  
   - **Not Rated**   : Belum diketahui isinya.
   - **G**           : Baik untuk semua umur.  
   - **Passed**      : Film disetujui sensor sebagai layak tayang publik.  
   - **Approved**    : Film dianggap dapat diterima untuk semua penonton oleh sensor.  
   - **18+**         : Bukan untuk anak-anak.
   - **Not Available**: Anda harus menonton untuk mengetahuinya sendiri.  
   - **TV-PG**       : Cukup baik untuk TV, cocok untuk acara TV keluarga.  
   - **Unrated**     : Belum dinilai oleh sensor, tonton dengan risiko sendiri.  
   - **X**           : XXX-rated, banyak s*ks dan ketelanjangan.  
   - **13+**         : Untuk pra-remaja dan remaja seperti PG-13 tapi untuk TV.  
   - **TV-MA**       : Hanya untuk dewasa banyak kekerasan, seks, dan bahasa kasar.  
   - **GP**          : Untuk semua penonton orangtua disarankan mendampingi.  



- **Exploratory Data Analysis - Rating**  
  Didapatkan insight bahwa sebagian besar rating berada di antara 8,1 – 8,3.

  - **Exploratory Data Analysis - World Cloud**  
  Dengan worldcloud kita bisa melihat bahwa crime, drama, comedy merupakan genre yang banyak digemari

- **Exploratory Data Analysis - Mengecek Missing Values**  
  didapatkan hasil 250 baris 13 colom dan tidak ada missing value juga. mantap, lanjut!


---

## DATA PREPARATION
Data preparation merupakan tahapan penting untuk memastikan kualitas data sebelum dilakukan pemodelan. Tahapan ini meliputi pembersihan data, transformasi, dan persiapan fitur sehingga algoritma content-based filtering dapat bekerja secara optimal.

### 1. Penanganan Duplikasi (Handling Duplicates)
- **Proses:** Menghapus baris duplikat berdasarkan kombinasi `name` dan `year`.  
- **Alasan:** Duplikasi dapat menyebabkan bias pada rekomendasi dan mempengaruhi perhitungan kesamaan antarfilm.

### 2. Penanganan Missing Value (Handling Missing Values)
- **Proses:**
  - Kolom `run_time` diubah ke menit dan diisi dengan median jika missing.  
  - Kolom `budget` dan `box_office` diubah menjadi angka dan diisi median jika missing.  
- **Alasan:** Missing value dapat mengganggu proses feature extraction, normalisasi, dan perhitungan kesamaan film.

### 3. Penanganan Outlier (Handling Outliers)
- **Proses:** Menerapkan **IQR capping** pada kolom numerik (`rating`, `year`, `run_time_mins`, `budget_num`, `box_office_num`, `rank`).  
- **Alasan:** Outlier dapat mempengaruhi perhitungan kesamaan film dan merusak normalisasi data numerik.

### 4. Penambahan / Update Data
- **Proses:** Menambahkan kolom `length_tagline` yang berisi panjang karakter dari tagline film.  
- **Alasan:** Informasi tambahan ini dapat menjadi fitur numerik yang mendukung sistem rekomendasi berbasis konten.

### 5. Encoding Data Kategorikal
- **Proses:** Melakukan **one-hot encoding** pada kolom `certificate`.  
- **Alasan:** Algoritma tidak dapat langsung menggunakan data kategorikal, sehingga perlu dikonversi menjadi format numerik.

### 6. Normalisasi / Standarisasi Data Numerik
- **Proses:** Menggunakan **Min-Max Scaling** untuk kolom numerik (`rating`, `year`, `run_time_mins`, `budget_num`, `box_office_num`, `rank`).  
- **Alasan:** Normalisasi memastikan setiap fitur numerik berada pada skala yang sama sehingga perhitungan kesamaan tidak bias pada fitur dengan range besar.

### 7. Feature Engineering
- **Proses:** 
  - Memisahkan multi-genre menjadi list (multi-label).  
  - Ekstraksi TF-IDF untuk kolom `tagline`, `casts`, `directors`, dan `writers`.  
- **Alasan:** Hal ini dilakukan untuk membangun feature matrix lengkap yang siap dipakai untuk training/rekomendasi.

### 8. Feature Selection (unsupervised: VarianceThreshold)
- **Proses:**
  - fitur dengan variansi < 0.00001 akan dihapus (hampir konstan).
  - terapkan seleksi ke dataset
  - menghasilkan mask boolean fitur yang dipertahankan.
  - daftar nama fitur yang lolos seleksi.
  - info jumlah fitur yang dipertahankan dibanding total.
- **Alasan:** Hal ini dilakukan untuk mengurangi noise & dimensi dataset supaya model lebih efisien.

### 9. Data Splitting
- **Proses:** 
  - Menentukan `primary_genre` sebagai genre utama tiap film.  
  - Mengelompokkan genre dengan jumlah film < 2 menjadi kategori "Other".  
  - Mengecek distribusi genre untuk memastikan minimal ada 2 sampel tiap kelas.  
  - Membagi dataset menjadi train dan test set (80:20) dengan stratifikasi berdasarkan `primary_genre_strat`.  
- **Alasan:** Hal ini dilakukan untuk menghindari error ketika stratify (karena stratify butuh minimal 2 sampel per kelas) dan menjaga distribusi genre tetap proporsional di train/test set.

---

## Model Development
Tahap modeling bertujuan membangun sistem rekomendasi film yang dapat memberikan **top-N recommendation** kepada pengguna berdasarkan fitur film yang tersedia. Dalam proyek ini, digunakan pendekatan **Content-Based Filtering**.

- **Deskripsi:**  
  Model ini menghitung kesamaan antara film berdasarkan fitur numerik, one-hot encoding kategori, multi-hot genre, dan TF-IDF dari kolom teks (tagline, casts, directors, writers).  
  Kesamaan dihitung menggunakan **cosine similarity**, dan film dengan skor kesamaan tertinggi diberikan sebagai rekomendasi.  

- **Proses:**
  1. Gabungkan semua fitur menjadi matriks fitur (`X_combined`).  
  2. Hitung cosine similarity antarfilm:  
     ```python
     from sklearn.metrics.pairwise import cosine_similarity
     similarity_matrix = cosine_similarity(X_combined)
     ```
  3. Untuk film input tertentu, ambil film dengan skor similarity tertinggi sebagai **Top-N Recommendation**. dan diapatkanlah hasil Sebagai berikut :

| input_movie                                 | top_n_recommendations                                                                                     |
|--------------------------------------------|---------------------------------------------------------------------------------------------------------|
| A Beautiful Mind                            | Rush, Ford v Ferrari, Hamilton, Green Book, C...                                                        |
| The Lord of the Rings: The Return of the King | The Lord of the Rings: The Fellowship of the Ring, ..., ...                                             |
| North by Northwest                          | Psycho, Rear Window, Spider-Man: No Way Home, ..., ...                                                  |
| The Shining                                 | Capernaum, Whiplash, The Shawshank Redemption, ..., ...                                                 |
| Up                                         | Inside Out, Monsters, Inc., Klaus, Coco, Spider-Man: ..., ...                                           |


- **Kelebihan:**
  - Rekomendasi sangat personal karena berdasarkan konten film.  
  - Tidak memerlukan data rating pengguna sebelumnya.  
  - Dapat memanfaatkan informasi numerik dan teks secara bersamaan.  

- **Kekurangan:**
  - Tidak dapat memberikan rekomendasi novel yang sangat berbeda dari film sebelumnya (cold-start untuk konten baru tetap sulit).  
  - Terbatas pada fitur yang tersedia; kualitas rekomendasi tergantung pada akurasi representasi fitur.  

**DEMO**
Hal ini dilakukan untuk menjalankan *demo rekomendasi* dengan film `"The Godfather"`.  

**Demo Recommendation: Sistem Rekomendasi Film**

Untuk menunjukkan bagaimana sistem rekomendasi bekerja, dilakukan demo dengan menggunakan film **"The Godfather"** sebagai film input. Sistem akan memberikan **Top-10 rekomendasi** berdasarkan kesamaan konten dan filter genre yang sama.

**Kode Demo**
```python
demo = recommend("The Godfather", top_n=10, filter_same_genre=True)
print(demo.head(10))
```

**Hasil Demo Recommendation: Like _The Godfather_ **

| Rank | Name                     | Year | Rating | Genres                     | Similarity   |
|------|--------------------------|------|--------|----------------------------|-------------|
| 1    | The Godfather Part II     | 1974 | 8.85   | Crime, Drama               | 0.883123    |
| 2    | Apocalypse Now            | 1979 | 8.50   | Drama, Mystery, War        | 0.637844    |
| 3    | Scarface                  | 1983 | 8.30   | Crime, Drama               | 0.592057    |
| 4    | Pulp Fiction              | 1994 | 8.85   | Crime, Drama               | 0.591636    |
| 5    | City of God               | 2002 | 8.60   | Crime, Drama               | 0.588853    |
| 6    | The Green Mile            | 1999 | 8.60   | Crime, Drama, Fantasy      | 0.574491    |
| 7    | American History X        | 1998 | 8.50   | Crime, Drama               | 0.573124    |
| 8    | Joker                     | 2019 | 8.40   | Crime, Drama, Thriller     | 0.566046    |
| 9    | The Silence of the Lambs  | 1991 | 8.60   | Crime, Drama, Thriller     | 0.558354    |
| 10   | Capernaum                 | 2018 | 8.40   | Drama                      | 0.553148    |


**Insight dari hasil rekomendasi:**  

1. **Top rekomendasi paling mirip**  
   - `The Godfather Part II` (8.85) → secara tematik dan genre (`Crime, Drama`) paling dekat dengan *The Godfather* → similarity 0.88, sangat tinggi.  
   
2. **Genre Crime & Drama mendominasi**  
   - Sebagian besar film rekomendasi termasuk `Crime, Drama`, seperti `Scarface`, `Pulp Fiction`, `City of God`.  
   - Menunjukkan algoritma berhasil memfilter berdasarkan genre yang sama (`filter_same_genre=True`).  

3. **Film dengan genre tambahan tapi relevan**  
   - `The Green Mile` menambahkan `Fantasy`, `Joker` & `The Silence of the Lambs` menambahkan `Thriller`.  
   - Meskipun ada sub-genre lain, masih dekat secara konten/tema → similarity masih cukup tinggi (0.55–0.57).  

4. **Rentang tahun bervariasi**  
   - Dari film klasik (`The Godfather Part II`, 1974) hingga modern (`Joker`, 2019), artinya sistem merekomendasikan berdasarkan konten & genre, bukan hanya tahun rilis.  

5. **Similarity score**  
   - Nilai tertinggi 0.88 → film sangat mirip.  
   - Nilai 0.55 → film masih relevan, tapi agak berbeda dari film asli.  
   - Memberikan gambaran “seberapa dekat” film lain dengan film referensi.  


---

## EVALUASI MODEL
Tahap evaluasi bertujuan menilai kualitas sistem rekomendasi film berdasarkan **top-N recommendation** yang dihasilkan. Evaluasi dilakukan menggunakan beberapa metrik standar pada sistem rekomendasi berbasis content-based filtering.

**1. Metrik Evaluasi**

**1.1 Precision@K**
- **Deskripsi:** Mengukur proporsi rekomendasi yang relevan dari top-K film yang direkomendasikan.  
- **Formula:**  
\[
\text{Precision@K} = \frac{\text{Jumlah film relevan di top-K}}{K}
\]  
- **Interpretasi:** Nilai tinggi menunjukkan model sangat tepat dalam memilih item yang benar.

**1.2 Recall@K**
- **Deskripsi:** Mengukur proporsi film relevan yang berhasil direkomendasikan dari total film relevan yang ada.  
- **Formula:**  
\[
\text{Recall@K} = \frac{\text{Jumlah film relevan di top-K}}{\text{Total film relevan}}
\]  
- **Interpretasi:** Nilai rendah menunjukkan model hanya menampilkan sebagian kecil dari semua item relevan.

**1.3 NDCG@K (Normalized Discounted Cumulative Gain)**
- **Deskripsi:** Mengukur kualitas ranking rekomendasi, memberi bobot lebih pada film relevan yang muncul di posisi atas.  
- **Formula:**  
\[
DCG@K = \sum_{i=1}^{K} \frac{2^{rel_i} - 1}{\log_2(i + 1)}, \quad
NDCG@K = \frac{DCG@K}{IDCG@K}
\]  
- **Interpretasi:** Nilai mendekati 1 menunjukkan urutan rekomendasi sangat optimal, film relevan ditempatkan di posisi teratas.

**2. Evaluation Metrics**

| Metric        | @5      | @10     | @20     |
|---------------|---------|---------|---------|
| Precision     | 0.9960  | 0.9880  | 0.9800  |
| Recall        | 0.0480  | 0.0942  | 0.1852  |
| NDCG          | 1.0000  | 0.9990  | 0.9975  |


**3. Hasil Evaluasi**
| Metrik       | Skor   | Insight                                                                 |
|--------------|--------|------------------------------------------------------------------------|
| Precision@K  | ≈0.99  | Hampir semua item yang direkomendasikan relevan → model sangat presisi.|
| Recall@K     | 0.05–0.18 | Hanya sebagian kecil dari item relevan yang ditampilkan → model kurang menjangkau semua item relevan.|
| NDCG@K       | ≈0.996 | Item relevan ditempatkan di posisi teratas → ranking rekomendasi sudah optimal.|

**Insight Keseluruhan:**  
- Model sangat **presisi**, sehingga rekomendasi yang muncul hampir semuanya relevan.  
- Recall rendah, artinya model belum mampu menjangkau semua item relevan.  
- Ranking rekomendasi sangat baik, terbukti dari NDCG yang mendekati 1, sehingga film relevan muncul di urutan atas list rekomendasi.


### KESIMPULAN

**Menjawab Problem Statements**
- **Problem 1:** Sistem rekomendasi berbasis **Content-Based Filtering** berhasil menampilkan film yang sesuai preferensi pengguna berdasarkan genre, cast, dan sutradara.  
- **Problem 2:** Rekomendasi personal yang sebelumnya hanya mengandalkan popularitas kini diperbaiki dengan memanfaatkan kesamaan konten antarfilm.  
- **Problem 3:** Pemrosesan fitur numerik dan teks (rating, year, durasi, budget, tagline, writers) efektif untuk menghitung kemiripan antarfilm, sehingga rekomendasi lebih relevan.

**Mencapai Goals yang Diharapkan**
- **Goal 1:** Content-Based Filtering berhasil memberikan rekomendasi **top-N film** yang relevan dan personalisasi, mempermudah pengguna menemukan film favorit.  
- **Goal 2:** Sistem memperhitungkan genre, pemeran, sutradara, dan fitur lainnya, meningkatkan personalisasi rekomendasi.  
- **Goal 3:** Feature engineering dan feature selection memaksimalkan penggunaan data film sehingga rekomendasi akurat dan konsisten.

**Dampak Solution Statements**
- **Content-Based Filtering (TF-IDF + Cosine Similarity):**  
  - Efektif untuk genre multi-film dan fitur teks (tagline, cast, directors, writers).  
  - Membantu memberikan rekomendasi untuk film baru atau kurang populer.  
- **Optimasi Fitur dan Evaluasi (Precision@K, Recall@K, NDCG@K):**  
  - Precision@K ≈0.99 → hampir semua rekomendasi relevan.  
  - Recall@K 0.05–0.18 → sebagian kecil item relevan muncul di top-N, dapat ditingkatkan.  
  - NDCG@K ≈0.996 → ranking rekomendasi optimal, item relevan muncul di posisi teratas.  
- **Demo Recommendation:**  
  - Sistem mampu menampilkan rekomendasi film mirip dengan film input (contoh: "The Godfather") dengan urutan ranking yang logis dan similarity yang menurun bertahap, mempermudah interpretasi pengguna.

**Insight Keseluruhan:**  
Sistem berhasil menyelesaikan masalah utama yang diidentifikasi, meningkatkan personalisasi rekomendasi, dan memaksimalkan pemanfaatan data fitur film. Pendekatan Content-Based Filtering dengan optimasi fitur dan evaluasi metrik memberikan rekomendasi yang akurat, relevan, dan mudah dipahami oleh pengguna.


### Pengembangan ke Depan

- Menggabungkan **Content-Based + Collaborative Filtering** menjadi sistem rekomendasi hybrid.  
- Meningkatkan antarmuka agar rekomendasi lebih interaktif dan personal.
