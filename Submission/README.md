
# Project Overview

Proyek ini berfokus pada pembangunan sistem rekomendasi film menggunakan The Movies Dataset dari Kaggle. Tujuan dari proyek ini adalah untuk membantu pengguna dalam menemukan film yang sesuai dengan preferensi mereka dengan memanfaatkan algoritma rekomendasi. 

Dengan jumlah konten yang terus bertambah di industri hiburan, sistem rekomendasi menjadi sangat penting untuk menawarkan saran yang dipersonalisasi kepada pengguna. Proyek ini bertujuan untuk mengimplementasikan pendekatan **Content-Based Filtering**, untuk mengatasi masalah dalam menemukan film yang ingin ditonton oleh pengguna berdasarkan preferensi pengguna.

**References:**
- The Movies Dataset: [Kaggle Link](https://www.kaggle.com/rounakbanik/the-movies-dataset)

# Business Understanding

### Problem Statements:
- Bagaimana kita dapat membangun sistem rekomendasi film yang memberikan saran film yang dipersonalisasi kepada pengguna?
- Seberapa akuratkah sistem rekomendasi yang dibangun untuk memberikan saran film yang relevan dan memuaskan bagi pengguna, sehingga dapat meningkatkan pengalaman pengguna dalam memilih konten yang sesuai dengan preferensi mereka? 

### Goals:
- Untuk mengembangkan sistem rekomendasi yang memberikan rekomendasi film yang akurat.
- Untuk mengimplementasikan pendekatan rekomendasi Content-Based Filtering.

### Solution Approach:
1. **Content-Based Filtering**: Pendekatan ini menggunakan metadata film (seperti genre, keywords) untuk merekomendasikan film yang serupa berdasarkan preferensi pengguna sebelumnya.

# Data Understanding

### Dataset:
- **Movies Metadata**: Berisi metadata untuk film seperti genre, judul, tanggal rilis, dll. Namun pada saat dimodeling hanya kolom `original_title`, `genres`, `vote_average`, `overview` dan `Id` saja
- **Keywords Dataset**: Berisi kata kunci yang terkait dengan film.

**Data Details**:
1. Metadata Film: 45.000+ barisdenagn 24 kolom, berbagai atribut termasuk genre, deskripsi film, tanggal rilis, dll. berikut adalah detail lengkap dari dataset Metadata Film:
- adult: Menunjukkan apakah film ditujukan untuk penonton dewasa atau tidak.
- belongs_to_collection: Berisi informasi tentang apakah film tersebut merupakan bagian dari sebuah koleksi atau waralaba (franchise). 
- budget: Anggaran produksi film dalam bentuk angka, tetapi disimpan sebagai string. 
- genres: Berisi informasi mengenai genre film dalam format JSON. 
- homepage: URL dari situs web resmi film, jika ada.
- id: ID unik untuk setiap film di dataset.
- imdb_id: ID film yang terdaftar di situs IMDb, yang dapat digunakan untuk pencarian di platform tersebut.
- original_language: Bahasa asli dari film.
- original_title: Judul asli film dalam bahasa aslinya, sebelum diterjemahkan atau diubah untuk pasar internasional.
- overview: Sinopsis singkat atau ringkasan dari plot film.
- popularity: Ukuran popularitas film di berbagai platform. 
- poster_path: Path ke poster film yang dapat digunakan untuk menampilkan gambar poster melalui situs TMDb.
- production_companies: Berisi nama perusahaan produksi film dalam format JSON.
- production_countries: Negara tempat film diproduksi, disimpan dalam format JSON.
- release_date: Tanggal rilis film. Biasanya dalam format YYYY-MM-DD.
- revenue: Pendapatan global yang dihasilkan oleh film, dalam dolar AS.
- runtime: Durasi film dalam menit.
- spoken_languages: Bahasa yang digunakan dalam film, disimpan dalam format JSON.
- status: Status produksi film.
- tagline: Slogan atau tagline dari film, yang sering kali digunakan dalam promosi.
- title: Judul resmi film yang mungkin berbeda dari judul aslinya (original_title).
- video: Menunjukkan apakah film tersebut memiliki trailer video (True atau False).
- vote_average: Skor rata-rata film berdasarkan penilaian dari pengguna.
- vote_count: Jumlah total suara atau penilaian yang diterima oleh film.
- 
2. Dataset Keywords: Memiliki 90.000+ baris dengan 2 kolom, berisi kata kunci yang terkait dengan film. berikut adalah detail lengkap dari dataset Keywords:
- id: ID unik untuk setiap film, yang sesuai dengan kolom id di dataset movie. Ini adalah kunci yang dapat digunakan untuk menghubungkan kedua dataset.
- keywords: Berisi kata kunci atau tag yang relevan dengan film, dalam format JSON. Kata kunci ini menggambarkan tema atau elemen utama dalam film.

3. Data Merge: Data ini dihasilkan dari gabungan data metadata film dan data keywords, dengan lebih dari 45000+ data baris dan 7 kolom. berikut adalah detail lengkap dari dataset Merge:
- id: ID unik untuk setiap film di dataset.
- original_title: Judul asli film dalam bahasa aslinya, sebelum diterjemahkan atau diubah untuk pasar internasional.
- genres: Berisi informasi mengenai genre film dalam format JSON.
- vote_average: Skor rata-rata film berdasarkan penilaian dari pengguna.
- overview: Sinopsis singkat atau ringkasan dari plot film.
- keywords: Berisi kata kunci atau tag yang relevan dengan film, dalam format JSON. Kata kunci ini menggambarkan tema atau elemen utama dalam film.


**Data dimuat dan dieksplorasi menggunakan `pandas`, dan beberapa kolom memiliki nilai yang hilang yang ditangani selama persiapan data dan setelah pembersihan data hanya sekitar 45463 yang terpakai untuk modeling*

### Data Source:
- [The Movies Dataset](https://www.kaggle.com/rounakbanik/the-movies-dataset)

# Data Preparation

Proses persiapan data melibatkan langkah-langkah berikut:
- Melakukan penggabungan dataset merge dengan menggabungkan antara data metadata filmdan data keywords dengan kolom yang digabungkan melalui kolom id
- Menangani nilai yang hilang dan duplikasi dalam set Movies Metadata, Keywords datasets dan datasets Merge.
- Melakukan pembersihan pada kolom `genres` dan `keywords` karna pada datasets Merge kolom tersebut nilai yang ada berupa format JSON, untuk itu dilakukan proses pembersihan pada kolom tersebut sehingga menghasilkan data yang berkualitas
- Mengekstrak fitur dengan melakukan pembuatan kolom baru bernama `tags` yang dihasilkan dari penggabungan beberapa kolom yaitu dari kolom `original_title`, `genres` & `keywords`
- Memvektorisasi data teks (data tags yang dihasilkan dari kombinasi title, genre, dan keywords) menggunakan **TF-IDF** untuk menghitung kemiripan.

Langkah-langkah ini diperlukan untuk memastikan bahwa data sudah bersih dan siap untuk tahap pemodelan, sehingga algoritme dapat menghasilkan rekomendasi yang akurat.

# Modeling and Result

Berikut adalah beberapa langkah dalam pembuatan sistem rekomendasi yang dibangun menggunakan pendekatan **Content-Based Filtering**:

1. **Content-Based Filtering**:
   - Menggunakan **TF-IDF Vectorizer** untuk mengekstrak fitur dari kolom tags.
   - Menerapkan **Cosine Similarity** untuk menemukan film yang paling mirip dengan preferensi pengguna.
   - Membuat fungsi dengan nama `recommend_movie` untuk menghasilkan 15 film rekomendasi berdasarkan preferensi user
   - Dengan metode yang digunakan ini efisien dalam merekomendasikan film dengan karakteristik yang serupa sesuai dengan yang user cari atau yang user minati.
   
### Top-15 Recommendations:
- Pendekatan **`Content-Based Filtering`** memberikan daftar Top-15 film yang direkomendasikan berdasarkan preferensi pengguna.

# Evaluation

### Evaluation Metrics:
1. **Cosine Similarity** digunakan untuk mengukur seberapa mirip film-film dalam hal atributnya (untuk pemfilteran berbasis konten).
2. **Precision** digunakan untuk mengevaluasi kinerja content-based filtering berdasarkan preferensi pengguna. Skor presisi yang dicapai adalah **73,3%**.”

Metrik ini dipilih karena sesuai dengan tujuan untuk merekomendasikan film berdasarkan kesamaan atau berdasarkan interaksi pengguna. 

### Conclusion:
Secara keseluruhan, model yang dikembangkan telah memberikan solusi yang cukup baik untuk problem statement, dengan precision 73,3% yang menunjukkan bahwa model ini mampu memberikan rekomendasi yang akurat. Model ini juga berhasil mencapai goals yang ditetapkan, meskipun ada ruang untuk perbaikan lebih lanjut guna meningkatkan presisi dan pengalaman pengguna.

Precision mengukur seberapa akurat rekomendasi yang diberikan model, yakni proporsi film yang direkomendasikan dan disukai pengguna dari semua yang disarankan. Nilai 73,3% menunjukkan bahwa sekitar 3 dari 4 film yang direkomendasikan sesuai dengan preferensi pengguna. Artinya, model berhasil memberikan rekomendasi yang relevan dan berkualitas dan menjawab kebutuhan untuk memberikan saran yang personal.
