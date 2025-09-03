# 📑 Laporan Proyek Akhir Machine Learning Terapan - Cendekia Luthfieta Nazalia

---

## DOMAIN PROYEK  
Rekomendasi film membantu pengguna menemukan film yang sesuai dengan preferensi mereka. Sistem ini menggunakan dataset IMDB Top 250 Movies dan memanfaatkan genre, rating, dan tahun rilis untuk memberikan rekomendasi.

Masalah ini penting karena:  
- Pengguna kesulitan menemukan film yang sesuai dengan minat mereka.
- Platform streaming dan aplikasi hiburan membutuhkan insight untuk personalisasi rekomendasi dan meningkatkan engagemen 

Referensi:  
- K. Ricci et al., Recommender Systems Handbook, 2nd Edition, Springer, 2015. 
- B. Sarwar et al., “Item-based collaborative filtering recommendation algorithms,” WWW Conference, 2001. 

---

## BUSINESS UNDERSTANDING

### Problem Statements  
1. Bagaimana memberikan rekomendasi film yang sesuai dengan preferensi pengguna berdasarkan genre, rating, dan tahun rilis?  
2. Bagaimana memanfaatkan data rating pengguna untuk meningkatkan akurasi rekomendasi film?

### Goals  
1. Membangun sistem rekomendasi film menggunakan Content-Based Filtering dan Collaborative Filtering (Item-Item). 
2. Memberikan rekomendasi film yang relevan dan personalisasi untuk setiap pengguna.
3. Menggunakan Nearest Neighbors untuk mendukung rekomendasi berbasis kemiripan numerik (tahun rilis dan rating).

### Solution Statements  
1. Menggunakan TF-IDF + Cosine Similarity untuk Content-Based Filtering berdasarkan multi-genre film.
2. Menggunakan Item-Item Collaborative Filtering dengan pivot user-movie ratings untuk menemukan film serupa.
3. Menggunakan Nearest Neighbors pada fitur numerik (year + tating) untuk rekomendasi berbasis jarak.
4. Menyediakan visualisasi similarity dan distribusi jarak neighbors untuk evaluasi dan insight model.

---

## DATA UNDERSTANDING 

Data yang digunakan pada proyek ini adalah **IMDB Top 250 Movies dataset (2021)** yang diunduh dari Kaggle.  
**Dataset**: [IMDB Top 250 Movies](https://www.kaggle.com/datasets/rajugc/imdb-top-250-movies-dataset)
Untuk tahap latihan, Anda hanya akan menggunakan dataset ini sehingga tidak perlu menambahkan data lain atau melakukan penggabungan dataset. Dataset ini cukup sederhana dan bersih sehingga tidak terlalu banyak memerlukan proses data cleaning. Dataset ini terdiri dari 250 movies data yang berisi informasi mengenai

- rank → Peringkat film
- name → Nama film
- year → Tahun rilis
- rating → Rating film
- genre → Genre film
- certificate → Sertifikat film (rating usia)
- run_time → Durasi total film
- tagline → Tagline film
- budget → Anggaran produksi
- box_office → Total pendapatan box office global
- casts → Semua pemeran film
- directors → Sutradara film
- writers → Penulis naskah film . 

Dataset ini memungkinkan kita untuk menganalisis:

- Tren industri film  
- Genre populer  
- Pola rating film  
- Faktor kesuksesan film  

Serta digunakan untuk membangun **sistem rekomendasi film yang interaktif dan personalisasi**.

Dalam membuat model dengan machine learning kita akan  menggunakan tools google colaboratory.

## EDA (Exploratory Data Analysis)  
- Univariate Exploratory Data Analysis - Deskripsi Variabel dilakukan dengan melihat informasi dataset `.info()` dan statistik deskriptif `.describe()`.   
- Exploratory Data Analysis - tujuannya untuk mengetahui Rata-rata Ratings berdasarkan Genre
- Exploratory Data Analysis - tujuannya untuk mengetahui 5 Film Teratas Berdasarkan Rating
- Exploratory Data Analysis - tujuannya untuk mengetahui5 Film Teratas Berdasarkan Genre
- Exploratory Data Analysis - tujuannya untuk mengetahui 5 Film Teratas Berdasarkan Casts
- Exploratory Data Analysis - tujuannya untuk mengetahui 5 Film Teratas Berdasarkan Directors
- Exploratory Data Analysis - tujuannya untuk mengetahui 5 Film Teratas Berdasarkan Penulis 
- Exploratory Data Analysis - Jumlah Certificate tujuannya untuk mengetahui jumlah certificate
- Exploratory Data Analysis - Rating tujuannya untuk mengetahui sebaran rating
- Exploratory Data Analysis - World Cloud Tujuannya untuk visualisasi kata/genre yang paling sering muncul di dataset film.

---

## DATA PREPROCESSING
Preprocessing pada proyek sistem rekomendasi film bertujuan untuk menyiapkan dataset agar siap digunakan pada semua model (Content-Based Filtering, Collaborative Filtering, dan Nearest Neighbors). Berikut langkah-langkah yang dilakukan:

1. Mengecek Missing Values
- **Tujuan:** Mengetahui apakah ada data yang hilang pada kolom penting seperti `Title`, `Genre`, `Rating`, atau `Year`.  
- **Manfaat:** Data yang hilang bisa menyebabkan error saat model menghitung similarity atau membuat pivot table. Dengan mengecek missing values, kita bisa menangani data yang tidak lengkap sebelum diproses.

2. Split Genre Menjadi Beberapa Kolom
- **Tujuan:** Memisahkan multi-genre yang ditulis dalam satu kolom (misal `"Action, Drama, Thriller"`) menjadi kolom terpisah (`genre_1`, `genre_2`, `genre_3`).  
- **Manfaat:** Mempermudah pemrosesan genre untuk **Content-Based Filtering**. Model bisa mengenali setiap genre secara individual.

3. Mengisi Missing Values
- **Tujuan:** Memberikan placeholder atau default value pada data yang kosong (misal `Unknown` untuk genre).  
- **Manfaat:** Menghindari error saat menghitung similarity atau membuat pivot table, serta menjaga konsistensi dataset.

4. Konversi Year & Rating ke Numerik
- **Tujuan:** Mengubah kolom `Year` dan `Rating` dari string ke tipe numerik (`int` atau `float`).  
- **Manfaat:** Diperlukan untuk perhitungan **Nearest Neighbors** dan analisis numerik. Tanpa konversi, model tidak bisa menghitung jarak antar film dengan benar.

5. Menghapus Duplikasi
- **Tujuan:** Menghilangkan baris film yang sama lebih dari sekali.  
- **Manfaat:** Mencegah bias atau pengaruh berlebih pada film tertentu saat menghitung similarity atau membuat rekomendasi.

**Kesimpulan:**  
Langkah preprocessing ini memastikan dataset bersih, konsisten, dan siap digunakan pada semua metode rekomendasi, sehingga menghasilkan output rekomendasi yang akurat dan handal.

---

## DATA PREPARATION  

Tahap **data preparation** bertujuan untuk menyiapkan dataset agar siap digunakan dalam semua metode rekomendasi (Content-Based Filtering, Collaborative Filtering, dan Nearest Neighbors). Berikut langkah-langkah yang dilakukan:

1. Menggabungkan Semua Genre
- **Tujuan:** Menggabungkan semua kolom genre (`genre_1`, `genre_2`, `genre_3`, ...) menjadi satu kolom `genre_combined`.  
- **Manfaat:** Mempermudah proses **Content-Based Filtering**, karena TF-IDF vectorizer membutuhkan satu kolom teks untuk menghitung similarity antar film.

2. Buat Pivot Table User-Movie (Simulasi User Rating)
- **Tujuan:** Membuat tabel pivot dengan baris sebagai `user_id`, kolom sebagai `Title`, dan nilai berupa rating atau skor simulasi.  
- **Manfaat:** Dibutuhkan untuk **Collaborative Filtering (Item-Item)** agar model bisa menghitung kemiripan antar film berdasarkan rating pengguna.  
- **Catatan:** Karena dataset asli tidak memiliki rating pengguna, kita menggunakan **simulasi rating** untuk latihan.

3. Menggunakan Fitur Numerik Year + Rating
- **Tujuan:** Memilih kolom `Year` dan `Rating` sebagai fitur numerik untuk model **Nearest Neighbors**.  
- **Manfaat:** Fitur numerik ini memungkinkan model menghitung jarak antar film dan memberikan rekomendasi berbasis kemiripan numerik (tahun rilis dan rating).

**Kesimpulan:**  
Data preparation ini memastikan semua fitur yang diperlukan tersedia dalam format yang sesuai untuk masing-masing metode rekomendasi, sehingga model dapat berjalan secara optimal dan menghasilkan rekomendasi yang relevan.


---

## Model Development

### Content-Based Filtering
**Cara Kerja:**  
Content-Based Filtering memberikan rekomendasi film berdasarkan **kemiripan genre** antar film. Model menggunakan **TF-IDF vectorizer** pada kolom `genre_combined` untuk mengubah teks menjadi vektor, lalu menghitung **cosine similarity** antar film. Film yang memiliki nilai similarity tertinggi dianggap paling relevan.  

**Parameter:**  
- TF-IDF vectorizer dengan stop_words='english'  
- Cosine similarity untuk mengukur kemiripan antar film  

**Kelebihan:**  
- Mudah dipahami dan diimplementasikan  
- Bisa merekomendasikan film baru selama genre diketahui  

**Kekurangan:**  
- Tidak mempertimbangkan rating atau preferensi pengguna  
- Tidak menangkap pola kolaboratif antar pengguna  

**Proses Training / Initialization:**  
- TF-IDF vectorizer 'fit' pada kolom `genre_combined`  
- Cosine similarity dihitung antar seluruh film  
- Tidak memerlukan split data karena unsupervised  

**Fungsi Rekomendasi:**  
- `get_content_recommendations(title)` mengambil film paling mirip berdasarkan cosine similarity  

---

### Collaborative Filtering
**Cara Kerja:**  
Collaborative Filtering berbasis item menggunakan **pivot table user-movie ratings**. Model menghitung **cosine similarity antar film** berdasarkan rating pengguna. Film yang memiliki pola rating serupa dianggap paling mirip, sehingga direkomendasikan kepada pengguna yang menyukai film tertentu.

**Parameter:**  
- Cosine similarity antar item (film)  
- Pivot table `user_movie_ratings` yang berisi rating pengguna (simulasi)  

**Kelebihan:**  
- Mempertimbangkan preferensi pengguna secara kolektif  
- Bisa menangkap film yang disukai pengguna lain dengan pola rating serupa  

**Kekurangan:**  
- Dataset asli tidak memiliki rating pengguna sehingga perlu simulasi  
- Tidak bisa merekomendasikan film baru yang belum diberi rating  

**Proses Training / Initialization:**  
- Membuat pivot table `user_movie_ratings` (user x movie)  
- Menghitung cosine similarity antar film  
- Model siap digunakan untuk mencari film serupa  

**Fungsi Rekomendasi:**  
- `get_item_based_recommendations(movie_title)` mengembalikan daftar film paling mirip berdasarkan item similarity  


---

## Proses Training Nearest Neighbors

**Cara Kerja:**  
Nearest Neighbors memberikan rekomendasi film berdasarkan **jarak numerik** antar film pada fitur `Year` dan `Rating`. Film yang paling dekat secara numerik dianggap paling mirip dan direkomendasikan.

**Parameter:**  
- `n_neighbors=10` untuk mengambil 10 film terdekat  
- `algorithm='ball_tree'` untuk efisiensi perhitungan jarak  

**Kelebihan:**  
- Mudah diterapkan pada fitur numerik  
- Memberikan rekomendasi berbasis kemiripan nyata (tahun rilis & rating)  

**Kekurangan:**  
- Hanya mempertimbangkan fitur numerik  
- Tidak memperhitungkan genre atau preferensi pengguna secara langsung  

**Proses Training / Initialization:**  
- Memilih fitur numerik `Year` dan `Rating` sebagai `X`  
- Membagi data menjadi `X_train` dan `X_test` (80%-20%)  
- Inisialisasi model `NearestNeighbors`  
- Melatih model dengan `X_train` (`nn_model.fit(X_train)`)  


**Fungsi Rekomendasi:**  
- Menggunakan `nn_model.kneighbors(X_test)` untuk mendapatkan indeks film terdekat  

---

## EVALUASI MODEL

### Metrik Evaluasi
- **Cosine Similarity (Content-Based Filtering & Collaborative Filtering)**  
  - Mengukur kemiripan antar film; nilai 1 = sangat mirip, 0 = tidak mirip.  
  - Digunakan untuk menentukan film rekomendasi teratas.

- **Jarak Neighbors (Nearest Neighbors)**  
  - Mengukur jarak Euclidean antar fitur numerik (`Year` + `Rating`).  
  - Rata-rata jarak digunakan untuk memeriksa sebaran kemiripan film.

### Hasil Evaluasi
- **Content-Based Filtering**  
  - Film rekomendasi untuk `'The Shawshank Redemption'` memiliki similarity tinggi (>0.5) dengan genre mirip.  
  - Heatmap 10 film pertama menunjukkan hubungan genre yang konsisten.

- **Collaborative Filtering (Item-Item)**  
  - Film rekomendasi untuk `'The Dark Knight'` memiliki pola rating pengguna yang mirip.  
  - Heatmap similarity menunjukkan beberapa film memiliki rating mirip yang tinggi antar pengguna simulasi.

- **Nearest Neighbors**  
  - Rata-rata jarak neighbors pada test samples bervariasi, sebagian besar film memiliki jarak <0.3 (fitur normalisasi).  
  - Plot distribusi jarak membantu memvisualisasikan sebaran kemiripan antar film secara numerik.

### Kesimpulan Evaluasi
- Content-Based Filtering efektif untuk genre multi-film dan rekomendasi film baru.  
- Collaborative Filtering (Item-Item) menangkap pola preferensi pengguna kolektif meski menggunakan rating simulasi.  
- Nearest Neighbors memberikan rekomendasi berbasis kemiripan numerik, memperkuat kualitas rekomendasi.  
- Visualisasi similarity dan distribusi jarak neighbors membantu memahami dan memvalidasi hasil model.

---


## KESIMPULAN
### Hasil Percobaan
Menjawab Problem Statements:

- **Problem 1:** Sistem rekomendasi berbasis Content-Based Filtering berhasil memberikan film yang sesuai preferensi pengguna berdasarkan genre.  
- **Problem 2:** Collaborative Filtering (Item-Item) mampu memanfaatkan data rating pengguna (simulasi) untuk meningkatkan akurasi rekomendasi.  
- **Problem 3:** Nearest Neighbors efektif dalam mendukung rekomendasi berbasis kemiripan numerik (tahun rilis dan rating).

### Mencapai Goals yang Diharapkan

- **Goal 1:** Content-Based Filtering dan Collaborative Filtering berhasil membangun sistem rekomendasi yang relevan dan personalisasi.  
- **Goal 2:** Nearest Neighbors memberikan insight tambahan untuk film yang mirip secara numerik, meningkatkan kualitas rekomendasi.  

### Dampak Solution Statements

- **Content-Based Filtering:** Menggunakan TF-IDF + Cosine Similarity efektif untuk genre multi-film, membantu rekomendasi untuk film baru.  
- **Collaborative Filtering (Item-Item):** Menggunakan pivot user-movie ratings membantu menangkap pola preferensi pengguna kolektif.  
- **Nearest Neighbors:** Memberikan rekomendasi berbasis jarak numerik dengan fitur `Year` dan `Rating`.  
- Visualisasi similarity dan distribusi jarak neighbors mempermudah interpretasi dan evaluasi model.

### Pengembangan ke Depan

- Menggabungkan **Content-Based + Collaborative Filtering** menjadi sistem rekomendasi hybrid.  
- Menambahkan fitur tambahan seperti durasi, bahasa, atau popularitas film.  
- Menggunakan dataset nyata dengan rating pengguna asli untuk Collaborative Filtering.  
- Meningkatkan antarmuka agar rekomendasi lebih interaktif dan personal.
