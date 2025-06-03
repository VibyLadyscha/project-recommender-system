# Laporan Proyek Machine Learning - Viby Ladyscha Yalasena Winarno

## Project Overview

Seiring dengan pesatnya pertumbuhan dunia penerbitan dan digitalisasi buku, pengguna dihadapkan pada tantangan memilih bacaan yang relevan dari ribuan bahkan jutaan judul yang tersedia. Kondisi ini dapat menyebabkan kelelahan dalam mengambil keputusan dan berkurangnya minat membaca karena kesulitan menemukan buku yang sesuai. Oleh karena itu, dibutuhkan sistem yang mampu secara otomatis menyaring dan merekomendasikan buku berdasarkan preferensi masing-masing pengguna. Sistem rekomendasi berperan penting dalam mengatasi permasalahan ini dengan menganalisis pola interaksi pengguna dan fitur konten dari buku.

Dua pendekatan utama dalam pengembangan sistem ini adalah Content-Based Filtering yang memanfaatkan kesamaan fitur buku seperti pengarang dan genre, serta Collaborative Filtering, yang mengidentifikasi pola pengguna lain dengan preferensi serupa [[1](https://onlinelibrary.wiley.com/doi/10.1155/2009/421425)]. Penggabungan kedua pendekatan melalui metode hybrid telah terbukti meningkatkan relevansi rekomendasi [[2](https://www.researchgate.net/publication/383320649_Personalized_Book_Recommendations_A_Hybrid_Approach_Leveraging_Collaborative_Filtering_Association_Rule_Mining_and_Content-Based_Filtering)]. Lebih lanjut, penerapan metode machine learning seperti Neural Collaborative Filtering juga menunjukkan hasil signifikan dalam meningkatkan akurasi prediksi rating pengguna [[3](https://arxiv.org/abs/1708.05031)].

Dengan meningkatnya kebutuhan akan personalisasi dalam dunia literasi digital, pengembangan sistem rekomendasi buku yang andal dan cerdas menjadi penting, tidak hanya dalam meningkatkan pengalaman pengguna, tetapi juga sebagai bagian dari solusi teknologi dalam pengelolaan informasi skala besar.

## Business Understanding

Pengembangan sistem rekomendasi buku memiliki potensi besar dalam meningkatkan pengalaman membaca pengguna, mengurangi beban informasi (*information overload*), dan membantu pembaca menemukan konten yang sesuai dengan preferensi mereka. Dalam era digital dan meningkatnya digitalisasi pustaka, jumlah judul buku yang tersedia terus bertambah, membuat pengguna kerap kesulitan dalam memilih bacaan yang relevan dan menarik minat mereka. Sistem rekomendasi mampu menyaring pilihan berdasarkan data historis dan karakteristik buku, memberikan saran personal yang lebih relevan dan efisien.

### Problem Statements

Berdasarkan latar belakang tersebut, beberapa masalah yang ingin diselesaikan dalam proyek ini adalah:
1. Bagaimana membangun sistem rekomendasi buku yang mengintegrasikan pendekatan *Content-Based Filtering* dan *Collaborative Filtering* untuk menghasilkan rekomendasi yang akurat dan relevan?
2. Algoritma rekomendasi mana yang memberikan performa terbaik dalam memprediksi preferensi pengguna berdasarkan karakteristik buku dan data historis interaksi pengguna?

### Goals

Tujuan dari proyek ini meliputi:
1. Mengembangkan sistem rekomendasi buku yang memanfaatkan pendekatan *Content-Based Filtering* dan *Collaborative Filtering* untuk memberikan saran bacaan yang personal dan kontekstual.
2. Membandingkan performa berbagai metode rekomendasi untuk menentukan strategi atau kombinasi algoritma terbaik dalam memaksimalkan relevansi hasil rekomendasi.

### Solution statements

1. Analisis Data dan Preprocessing
   - Analisis Eksploratif dilakukan untuk menjelajahi dataset untuk memahami struktur data, kontribusi penulis, dan popularitas buku.
   - Pembersihan Data dilakukan untuk menangani *missing values* dan duplikasi pada dataset.
   - Encoding Fitur dilakukan untuk mengubah kolom seperti nama penulis dan id pengguna menjadi bentuk numerik menggunakan metode TF-IDF untuk pemrosesan lebih lanjut.
2. Implementasi Model *Content-Based Filtering*
   - Ekstraksi Fitur Buku menggunakan informasi seperti judul, penulis, dan deskripsi untuk membentuk representasi konten setiap buku.
   - TF-IDF Vectorization untuk mengubah teks deskripsi atau metadata buku menjadi representasi vektor menggunakan teknik TF-IDF.
   - Perhitungan Similaritas menggunakan *cosine similarity* untuk menghitung kesamaan antara buku dan merekomendasikan buku yang serupa dengan yang telah dibaca atau disukai pengguna.
3. Implementasi Model *Collaborative Filtering*
   - Pendekatan berbasis *User-Based Filtering* yaitu merekomendasikan buku yang belum dibaca pengguna berdasarkan kesamaan preferensi dengan pengguna lain.
   - Pendekatan berbasis model Menggunakan teknik seperti *matrix factorization* dengan algoritma seperti *RecommenderNet* untuk menangkap hubungan kompleks antara pengguna dan buku.

## Data Understanding

Pada proyek ini saya menggunakan data sekunder yang diunduh dari situs dataset *online* Kaggle dengan judul “[Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/data)”. Dataset disimpan dalam file dengan format .CSV yang kemudian akan digunakan dalam proses pengolahan data. Dataset ini terdiri dari 3 file berbeda yaitu Books.csv, Users.csv, dan Ratings.csv dengan kolom yang berbeda juga.

1. Books.csv
   
   Variabel yang tersedia:
   | Variabel             | Deskripsi                                                                                   |
   |----------------------|---------------------------------------------------------------------------------------------|
   | ISBN                 | Nomor ISBN unik untuk mengidentifikasi setiap buku. ISBN yang tidak valid telah dihapus.   |
   | Book-Title           | Judul buku.                                                                                 |
   | Book-Author          | Nama penulis buku. Jika terdapat beberapa penulis, hanya penulis pertama yang dicantumkan. |
   | Year-Of-Publication  | Tahun terbit buku.                                                                          |
   | Publisher            | Nama penerbit buku.                                                                         |
   | Image-URL-S          | URL ke gambar sampul buku berukuran kecil dari Amazon.                                     |
   | Image-URL-M          | URL ke gambar sampul buku berukuran sedang dari Amazon.                                    |
   | Image-URL-L          | URL ke gambar sampul buku berukuran besar dari Amazon.                                     |

   - `data_books` yang memuat file Books.csv memiliki dimensi (271360, 8) yang berarti memiliki baris sebanyak 271.360 data dan kolom sebanyak 8.
   - Setelah dilakukan pengecekan terhadap kolom yang ada pada `data_books`, kemudian dilakukan penghapusan pada kolom yang tidak relevan yaitu kolom `Image-URL-S`, `Image-URL-M` dan `Image-URL-L`.
   - Tipe data pada `data_books` merupakan object dengan total kolom setelah penghapusan sebanyak 5 kolom.
   - Setelah dilakukan pengecekan *missing value*, ternyata terdapat beberapa *missing value* pada kolom `Book-Author` dan `Publisher` sehingga perlu dilakukan penanganan pada tahap praproses data.
   - Setelah dilakukan pengecekan duplikat, ternyata tidak ada indikasi duplikat pada dataset buku.
   - Dilakukan pengecekan terhadap top 10 penulis dengan buku terbanyak

     ![top-10-penulis](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/top%2010%20penulis.png)

     Berdasarkan gambar di atas, dapat dilihat top 10 penulis dengan jumlah buku terbanyak. Penulis `Agatha Christie` memiliki jumlah buku terbanyak yaitu sekitar 600 buku.
   
2. Ratings.csv

   Variabel yang tersedia:
   | Variabel     | Deskripsi                                                                                                    |
   |--------------|--------------------------------------------------------------------------------------------------------------|
   | User-ID      | ID unik untuk setiap pengguna yang memberikan penilaian terhadap buku.                                       |
   | ISBN         | Nomor ISBN dari buku yang diberi penilaian.                                                                 |
   | Book-Rating  | Nilai rating buku. Nilai eksplisit berkisar dari 1 hingga 10 (semakin tinggi berarti semakin disukai), sedangkan nilai 0 menunjukkan penilaian implisit (misalnya hanya melihat atau mengakses tanpa memberi rating).    |

   - `data_ratings` yang memuat file Ratings.csv memiliki dimensi (1149780, 3) yang berarti memiliki baris sebanyak 1.149.780 data dan kolom sebanyak 3.
   - Tipe data pada `data_ratings` merupakan int64 dan object dengan total 3 kolom.
   - Setelah dilakukan pengecekan *missing values*, ternyata tidak ada indikasi *missing values* pada dataset rating.
   - Setelah dilakukan pengecekan duplikat, ternyata tidak ada indikasi duplikat pada dataset rating.
   - Dilakukan pengecekan terkait pengguna yang memberikan rating terhadap buku lebih dari satu kali.

     ![pengguna-lebih-satu](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/Screenshot%202025-06-01%20193918.png)

     Dapat dilihat bahwa terdapat 105.283 pengguna yang memberikan rating terhadap buku lebih dari satu kali.

3. Users.csv

   Variabel yang tersedia:
   | Variabel  | Deskripsi                                                                                                   |
   |-----------|-------------------------------------------------------------------------------------------------------------|
   | User-ID   | ID pengguna yang telah dianonimkan dan direpresentasikan sebagai bilangan bulat.                           |
   | Location  | Lokasi geografis pengguna (biasanya dalam format "kota, negara bagian, negara").                           |
   | Age       | Usia pengguna. Jika data tidak tersedia, nilai ini akan berisi NULL (kosong).                             |

   - `data_users` yang memuat file Users.csv memiliki dimensi (278858, 3) yang berarti memiliki baris sebanyak 278.858 data dan kolom sebanyak 3.
   - Tipe data pada `data_users` merupakan int64, float64, dan object dengan total 3 kolom.
   - Setelah dilakukan pengecekan *missing values*, ternyata terdapat beberapa *missing value* pada kolom `Age` sehingga perlu dilakukan penanganan pada tahap praproses data.
   - Setelah dilakukan pengecekan duplikat, ternyata tidak ada indikasi duplikat pada dataset user.

4. Data Final
   
   Setelah dilakukan penggabungan data final, dilakukan juga visualisasi terhadap 10 buku dengan jumlah rating terbanyak untuk memahami pola distribusi rating dalam data.

   ![pengguna-lebih-satu](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/top%2010%20buku.png)

   Berdasarkan gambar di atas, dapat dilihat top 10 buku dengan jumlah rating terbanyak yang diberikan oleh pengguna. Buku `Wild Animus` memiliki jumlah rating terbanyak dari pengguna yaitu sekitar 450.

## Data Preparation

### Penghapusan Kolom yang Tidak Relevan

- Pada tahap ini, dilakukan penghapusan pada kolom yang tidak relevan pada `data_books` yaitu kolom `Image-URL-S`, `Image-URL-M` dan `Image-URL-L`.
- Tujuan penghapusan kolom adalah untuk mengurangi dimensi data dan menghindari informasi yang tidak relevan (*noise*) sehingga proses komputasi menjadi lebih efisien dan performa model rekomendasi tidak terganggu.

### Filter Users yang Memberikan Rating > 150

- Pada tahap ini, dilakukan filter terhadap pengguna yang telah memberikan lebih dari 150 penilaian (rating) terhadap buku.
- Filtering ini dilakukan untuk memfokuskan pada pengguna yang aktif, sehingga data yang digunakan dalam pelatihan model berasal dari pengguna yang memiliki preferensi yang lebih terdefinisi, serta mengurangi *noise* dari pengguna yang hanya memberi sedikit atau satu penilaian.

### Menggabungkan Dataset Ratings dan Books

- Dataset `data_ratings` digabungkan dengan `data_books` berdasarkan kolom `ISBN` sebagai key.
- Tujuan dari penggabungan ini adalah untuk melengkapi data penilaian dengan informasi tambahan seperti judul buku, penulis, penerbit, dan tahun terbit agar sistem rekomendasi dapat memanfaatkan informasi berbasis konten (*Content-Based Filtering*).

### Perhitungan Jumlah Rating

- Dilakukan agregasi untuk menghitung jumlah rating yang diberikan pada masing-masing buku.
- Informasi ini berguna untuk mengidentifikasi buku mana yang populer (sering diberi rating) dan juga sebagai dasar untuk memfilter buku dengan jumlah rating terlalu sedikit yang mungkin tidak cukup representatif untuk dianalisis.

### Membuat Dataset Final

- Dataset `data_ratings_with_books` digabungkan dengan hasil agregasi jumlah rating (`num_ratings`) berdasarkan `Book-Title`.
- Dataset difilter agar hanya menyisakan buku yang memiliki minimal 50 rating karena buku dengan sedikit rating cenderung tidak cukup informasi untuk memberikan rekomendasi yang akurat.
- Duplikat kombinasi `User-ID` dan `Book-Title` dihapus untuk menghindari bias pada pengguna yang memberi rating ganda terhadap satu buku.
- Setelah proses pembersihan, diperoleh data final yang konsisten dan bebas duplikasi.

### Penghapusan Duplikasi ISBN

- Ditemukan bahwa satu ISBN bisa terkait dengan lebih dari satu judul buku, sehingga dilakukan penghapusan duplikasi berdasarkan ISBN.
- Hasil dari proses ini disimpan dalam variabel `preparation` yang digunakan untuk memastikan hanya satu entri unik per ISBN digunakan dalam sistem rekomendasi.
- Selanjutnya, data seperti `ISBN`, `Book-Title`, `Book-Author`, `Year-Of-Publication`, dan `Publisher` dikonversi menjadi list untuk mempermudah proses pemodelan selanjutnya.

### Data Preparation untuk Content-Based Filtering

1. Persiapan Data dan TF-IDF Vectorizer pada Kolom Book_Author
   - Dataset disalin ke variabel `data` untuk menjaga data asli tetap utuh.
   - Menggunakan `TfidfVectorizer` dari scikit-learn untuk mengubah teks penulis buku (`Book_Author`) menjadi representasi vektor numerik berdasarkan frekuensi dan pentingnya kata.
   - Bertujuan untuk mengekstrak fitur-fitur teks yang bermakna dari kolom penulis buku sehingga model dapat mengenali pola dan ciri khas penulis sebagai dasar perbandingan antar buku.
   
2. Membentuk DataFrame TF-IDF
   - Matriks TF-IDF yang berbentuk sparse matrix diubah ke bentuk dense untuk memudahkan visualisasi.
   - Membuat DataFrame dengan baris sebagai judul buku (`Book_Title`) dan kolom sebagai fitur nama penulis.
   - Bertujuan untuk memvisualisasikan representasi fitur numerik dari tiap buku sehingga memudahkan pemahaman distribusi fitur dan mempersiapkan data untuk proses kemiripan antar buku.

### Data Preparation untuk Collaborative Filtering

1. Encoding Kolom `User-ID` dan `ISBN`
   - Langkah pertama adalah mengubah `User-ID` dan `ISBN` menjadi representasi numerik (integer) menggunakan proses encoding.
   - `User-ID` dan `ISBN` diubah menjadi indeks integer unik melalui pembuatan dictionary:
   - `user_to_user_encoded` untuk memetakan ID pengguna ke angka.
   - `isbn_to_isbn_encoded` untuk memetakan ISBN buku ke angka.
   - Proses ini penting karena model machine learning biasanya memerlukan input dalam bentuk numerik, bukan string.

2. Mapping ke DataFrame
   - Setelah melakukan encoding, kolom baru `user` dan `book_title` ditambahkan ke dataframe:
   - `user` merupakan hasil pemetaan `User-ID` ke angka.
   - `book_title` merupakan hasil pemetaan `ISBN` ke angka.
   - Hal ini bertujuan untuk menyiapkan data input dalam format `[user, book]` agar bisa digunakan sebagai pasangan input dalam model rekomendasi.

3. Konversi Tipe dan Statistik Rating
   - Rating dikonversi ke tipe data `float32` untuk memastikan kompatibilitas dengan model TensorFlow/PyTorch.
   - Jumlah total pengguna dan buku dihitung untuk mengetahui dimensi input.
   - Nilai minimum dan maksimum rating diambil untuk digunakan dalam proses normalisasi.

4. Pengacakan Data
   - Data diacak menggunakan `df.sample(frac=1)` untuk memastikan distribusi rating tidak berpola saat dibagi menjadi data training dan validasi.
   - Pengacakan penting untuk menghindari bias urutan data saat pelatihan.

5. Pembagian Data: Training dan Validation
   - Data dibagi ke dalam 80% untuk training dan 20% untuk validation.
   - Fitur `x` berisi pasangan `[user, book_title]`.
   - Label `y` merupakan nilai rating yang telah dinormalisasi ke rentang 0-1 menggunakan rumus:
     
     $$\text{normalized rating} = \frac{\text{rating} - \text{min rating}}{\text{max rating} - \text{min rating}}$$
     
   - Proses normalisasi membantu model belajar lebih stabil karena seluruh label berada dalam skala seragam.

## Modeling

### Content-Based Filtering

Algoritma *Content-Based Filtering* yang digunakan dalam proyek ini bekerja dengan membandingkan kesamaan antar buku berdasarkan fitur `Book_Author` yang telah diubah menjadi representasi numerik. Langkah pertama adalah menghitung *Cosine Similarity* antar buku dengan menggunakan matriks fitur dari data training. Selanjutnya, fungsi `book_recommendation` digunakan untuk mencari buku yang paling mirip dengan buku yang diberikan sebagai input `Book_Title`. Fungsi ini mengidentifikasi indeks buku yang sesuai dengan judul yang dimasukkan, menghitung skor kesamaan dengan semua buku lainnya, dan menyusun daftar buku yang paling mirip berdasarkan skor tersebut.

Algoritma *Content-Based Filtering* dimulai dengan mengekstrak fitur `Book_Author` yang diubah menjadi representasi numerik menggunakan teknik seperti *CountVectorizer* atau TF-IDF. Fitur ini kemudian digunakan dalam membentuk matriks fitur di mana setiap baris mewakili satu buku sementara setiap kolom mewakili nama penulis yang menjadi dasar untuk menghitung kesamaan antar buku. Kesamaan dihitung dengan menggunakan `Cosine Similarity` yang mengukur sudut antara dua vektor dengan nilai berkisar antara 0 (tidak ada kesamaan) hingga 1 (identik). Setelah itu, algoritma mencari indeks buku sesuai dengan judul yang diberikan agar dapat mengakses skor kesamaan buku tersebut dengan buku lainnya, kemudian diurutkan secara menurun untuk menemukan buku paling relevan. Selanjutnya, algoritma memilih sejumlah buku teratas untuk direkomendasikan, mengambil data tambahan seperti `Book_Title` dan `Book_Author`. Hasil rekomendasi akhirnya disusun dalam bentuk tabel atau DataFrame. Dengan demikian, algoritma ini mampu memberikan rekomendasi buku yang relevan berdasarkan atribut yang mirip dengan buku input.

Kelebihan dari pendekatan ini adalah sistem dapat memberikan rekomendasi berdasarkan atribut yang relevan dengan buku yang disukai pengguna, tanpa memerlukan data interaksi dari pengguna lain. Ini memungkinkan sistem untuk bekerja bahkan untuk pengguna baru yang belum memberikan interaksi. Selain itu, *Content-Based Filtering* memberikan rekomendasi yang lebih personal karena didasarkan pada kesamaan fitur dari buku itu sendiri. Namun, kekurangannya adalah pendekatan ini hanya mengandalkan atribut yang ada, sehingga dapat menghasilkan rekomendasi yang terbatas atau kurang variatif, terutama jika buku yang memiliki kesamaan fitur terbatas. Selain itu, *Content-Based Filtering* sering kali mengalami masalah ketika ada buku dengan penulis yang tidak mencolok sehingga mengurangi kualitas rekomendasi.

#### Hasil Rekomendasi Buku

Rekomendasi telah berhasil dibuat untuk pengguna dengan judul buku input `Sea Swept (Quinn Brothers (Paperback))`.

Top 5 Rekomendasi Buku

| No | Book_Title                                              | Book_Author   |
|----|---------------------------------------------------------|---------------|
| 1  | Inner Harbor (Quinn Brothers (Paperback))               | Nora Roberts  |
| 2  | Carolina Moon                                           | Nora Roberts  |
| 3  | Midnight Bayou                                          | Nora Roberts  |
| 4  | Three Fates                                             | Nora Roberts  |
| 5 | Dance upon the Air (Three Sisters Island Trilogy)       | Nora Roberts  |

Berdasarkan output di atas, sistem berhasil merekomendasikan 5 judul buku teratas dengan kategori nama penulis buku (Nora Roberts) yang sama seperti penulis pada judul buku yang diinput.

### Collaborative Filtering

*Collaborative Filtering* merupakan metode rekomendasi yang bekerja dengan menganalisis pola interaksi antara pengguna dan item (buku), untuk memberikan rekomendasi yang sesuai dengan preferensi pengguna. Pada proyek ini, langkah awal adalah melakukan encoding terhadap User-ID dan ISBN, sehingga setiap pengguna dan buku direpresentasikan dalam bentuk angka unik. Selanjutnya, data dibagi menjadi dua set yaitu data training (80%) dan data validation (20%). Model yang digunakan yaitu `RecommenderNet`, dirancang dengan pendekatan embedding yang memetakan setiap pengguna dan buku ke dalam ruang vektor berdimensi tertentu yang ditentukan oleh parameter embedding_size. Embedding ini merepresentasikan karakteristik pengguna dan buku dalam bentuk vektor numerik. Model memiliki empat komponen utama yaitu embedding untuk pengguna `user_embedding` dan buku `book_title_embedding`, serta bias untuk pengguna `user_bias` dan buku `book_title_bias`. Dalam proses prediksi, model menghitung produk titik (*dot product*) antara vektor pengguna dan buku, kemudian menambahkan bias untuk mendapatkan nilai prediksi rating. Nilai ini dihitung menggunakan fungsi aktivasi sigmoid, yang menghasilkan output dalam rentang 0 hingga 1. Model dilatih menggunakan algoritma optimasi Adam dengan *learning_rate* sebesar 0.0001, dan fungsi loss yang digunakan adalah *Binary Crossentropy* untuk meminimalkan kesalahan prediksi. Selama pelatihan, performa model dievaluasi menggunakan metrik *Root Mean Squared Error* (RMSE) yang mengukur seberapa baik model memprediksi rating.

Parameter yang digunakan dalam algoritma *Collaborative Filtering* pada proyek ini diantaranya:
1. Jumlah Pengguna `num_users` merujuk pada total pengguna unik dari proses encoding kolom User-ID yang menentukan dimensi untuk embedding pengguna.
2. Jumlah Buku `num_book_title` adalah total buku unik dari encoding kolom ISBN yang menentukan dimensi untuk embedding buku.
3. Ukuran Embedding `embedding_size` ditetapkan pada 50 yang mewakili pengguna dan buku dalam vektor berdimensi 50.
4. Tingkat Pembelajaran `learning_rate` diatur pada 0.0001 akan mempengaruhi kecepatan pembaruan bobot model.
5. Fungsi Kehilangan `loss` menggunakan *Binary Crossentropy* untuk menghitung kesalahan antara rating prediksi dan aktual.
6. Metrik Evaluasi `metrics` menggunakan *Root Mean Squared Error* (RMSE) untuk menilai performa model.
7. Ukuran Batch `batch_size` ditetapkan pada 128 untuk memastikan efisiensi pelatihan pada dataset.
8. Jumlah Epoch `epochs` adalah 50, cukup untuk belajar tanpa overfitting.
9. Regularisasi `embeddings_regularizer` menggunakan L2 dengan nilai penalti 1×10^-6 untuk mengurangi risiko overfitting.
10. Fungsi Aktivasi `tf.nn.sigmoid` membatasi prediksi antara 0 dan 1 untuk menghasilkan probabilitas.

Semua parameter bekerja sama untuk mengoptimalkan pelatihan dan menghasilkan rekomendasi yang akurat berdasarkan interaksi antara pengguna dan buku.

Kelebihan dari pendekatan *Collaborative Filtering* ini adalah model dapat memberikan rekomendasi yang sangat personal dengan memanfaatkan data interaksi pengguna tanpa membutuhkan informasi tambahan tentang buku, seperti penerbit atau deskripsi buku. Pendekatan ini juga mampu menangani masalah *sparsity* (kurangnya data) dengan mengandalkan kesamaan antar pengguna atau buku. Namun, ada beberapa kekurangan seperti masalah *cold start*, di mana model kesulitan memberikan rekomendasi untuk pengguna atau buku baru yang tidak memiliki cukup interaksi sebelumnya. Selain itu, *Collaborative Filtering* juga rentan terhadap masalah skala besar, di mana model mungkin membutuhkan waktu dan sumber daya yang banyak untuk memproses data dengan jutaan pengguna dan film.

#### Hasil Rekomendasi Buku

Rekomendasi telah berhasil dibuat untuk pengguna dengan id 228998.

![rekomendasi-cf](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/Screenshot%202025-06-01%20184236.png)

Top 10 Rekomendasi Buku

| No | Book Title                                                  | Book Author      |
|----|-------------------------------------------------------------|------------------|
| 1  | The Hobbit : The Enchanting Prelude to The Lord of the Rings | J.R.R. TOLKIEN   |
| 2  | Charlotte's Web (Trophy Newbery)                            | E. B. White      |
| 3  | To Kill a Mockingbird                                       | Harper Lee       |
| 4  | Harry Potter and the Chamber of Secrets (Book 2)            | J. K. Rowling    |
| 5  | Harry Potter and the Prisoner of Azkaban (Book 3)           | J. K. Rowling    |
| 6  | Harry Potter and the Goblet of Fire (Book 4)                | J. K. Rowling    |
| 7  | Harry Potter and the Sorcerer's Stone (Book 1)              | J. K. Rowling    |
| 8  | Insomnia                                                    | Stephen King     |
| 9  | Seven Up (A Stephanie Plum Novel)                           | Janet Evanovich  |
| 10 | Fingersmith                                                 | Sarah Waters     |

## Evaluation

Pada proyek ini, terdapat dua evaluasi dari *Content-Based Filltering* dan *Collaborative Filltering*, berikut merupakan penjelasannya:

### Content-Based Filtering

Evaluasi model *Content-Based Filtering* dilakukan menggunakan tiga metrik utama yaitu *Precision*, *Recall*, dan *F1-Score*. Ketiga metrik ini secara umum digunakan untuk mengukur kinerja sistem rekomendasi.

*Precision* adalah bagian dari hasil positif yang diprediksi dengan benar. Metrik ini menunjukkan seberapa *confident* suatu model dalam memprediksi kelas positif sebagai positif. *Precision* dapat dihitung dengan rumus:

$$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}\%$$

Sedangkan, *recall* adalah metrik yang mengukur seberapa akurat suatu model memprediksi hasil positif. *Recall* dapat dihitung dengan rumus:

$$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}\%$$

*F1-Score* didapatkan dari rata-rata harmonis dari *precision* dan *recall*. Rata-rata harmonis ini tidak hanya memperhatikan nilai prediksi yang benar, tetapi juga memperhatikan nilai prediksi yang salah. Metrik *F1-Score* dapat dihitung dengan rumus:

$$\text{F1 Score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

Sebelum ketiga metrik tersebut dihitung, diperlukan data label aktual atau *ground truth* yang menjadi acuan dalam mengevaluasi prediksi model. Dalam konteks proyek ini, *ground truth* dibentuk berdasarkan hasil *cosine similarity* antar item, di mana setiap baris dan kolom pada matriks mewakili judul buku dan nilai pada setiap sel menunjukkan tingkat kemiripan. Nilai 1 diberikan jika dua item dianggap mirip dan 0 jika tidak mirip. Oleh karena itu, penetapan *threshold* menjadi penting untuk menentukan kapan dua item dinyatakan mirip atau tidak dalam proses evaluasi.

#### Interpretasi Hasil

![evaluasi-cbf](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/Screenshot%202025-06-01%20172116.png)

Berdasarkan hasil evaluasi pada model *Content-Based Filtering*, diperoleh nilai yang sangat tinggi untuk ketiga metrik evaluasi, yaitu *precision*, *recall*, dan *F1-Score*. *Precision* memiliki nilai 1.0, yang menunjukkan bahwa semua prediksi positif yang dihasilkan model benar adanya, tanpa adanya kesalahan klasifikasi positif (*false positive*). *Recall* juga mencapai nilai 1.0, yang berarti model mampu mengenali seluruh item relevan secara sempurna. *F1-Score* yang juga berada di angka 1.0 mencerminkan bahwa model memiliki keseimbangan yang optimal antara *precision* dan *recall*. Dengan demikian, dapat disimpulkan bahwa model mampu memberikan rekomendasi dengan performa yang sangat baik menggunakan pendekatan *Content-Based Filtering*.

### Collaborative Filtering

Model *Collaborative Filltering* menggunakan metrik RMSE (*Root Mean Square Error*) untuk mengevaluasi kinerja model yang dihasilkan. RMSE merupakan salah satu metode yang paling umum digunakan untuk mengukur kesalahan dalam model prediktif, khususnya ketika berurusan dengan data kuantitatif. Dengan menggunakan RMSE, dapat secara efektif menilai seberapa baik model dalam memprediksi nilai-nilai yang diharapkan berdasarkan data yang telah diamati sebelumnya. RMSE dapat dihitung dengan rumus berikut:

$$\text{RMSE} = \sqrt{ \frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2 }$$

Keterangan :
- RMSE = nilai *Root Mean Square Error*
- y = nilai hasil observasi
- ŷ = nilai hasil prediksi
- i = urutan data
- n = jumlah data

#### Interpretasi Hasil

![evaluasi-cf](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/collaborative%20filtering_rmse.png)

Setelah melakukan pelatihan model *Collaborative Filtering*, dapat dilihat bahwa plot metrik RMSE yang menunjukkan kinerja model dalam bentuk grafik. Dari plot tersebut, model menghasilkan nilai RMSE sebesar 0.2915 pada train dan 0.3136 pada validation. Angka ini menunjukkan bahwa kinerja model sudah cukup baik karena nilai RMSE yang lebih rendah menunjukkan kesalahan yang lebih kecil dalam prediksi.

## Summary

Hasil dari proyek ini menunjukkan bahwa pendekatan *Content-Based Filtering* dan *Collaborative Filtering* yang diimplementasikan telah memberikan kontribusi signifikan terhadap pemenuhan tujuan bisnis yang telah ditetapkan. Evaluasi performa model menunjukkan bahwa sistem mampu memberikan rekomendasi yang akurat, relevan, dan sesuai dengan kebutuhan pengguna. Sistem rekomendasi telah berhasil dikembangkan dengan dua pendekatan utama yaitu *Content-Based Filtering* dan *Collaborative Filtering*. Masing-masing pendekatan memberikan hasil rekomendasi yang personal dan kontekstual, sesuai dengan karakteristik pengguna maupun fitur buku, sehingga mencerminkan integrasi metode yang efektif. Evaluasi model menunjukkan bahwa pada *Content-Based Filtering* memberikan hasil sempurna pada metrik *Precision*, *Recall*, dan *F1-Score* yang semuanya bernilai 1.0, menandakan akurasi sangat tinggi dalam memberikan rekomendasi berdasarkan kesamaan konten. Sedangkan pada *Collaborative Filtering* menunjukkan kinerja yang baik dengan nilai RMSE yang rendah yaitu 0.2915 pada *train* dan 0.3136 pada *validation*, menandakan kesalahan prediksi yang kecil dalam mempelajari preferensi pengguna. Hal ini menunjukkan bahwa kedua algoritma memiliki keunggulan masing-masing tergantung pada konteks pengguna dan ketersediaan data. Sistem berhasil memberikan rekomendasi berdasarkan penulis (*Content-Based Filtering*) dan berdasarkan pola interaksi pengguna (*Collaborative Filtering*) yang menghasilkan saran bacaan yang personal dan sesuai preferensi masing-masing pengguna. Evaluasi komprehensif telah dilakukan menggunakan metrik yang sesuai yaitu *Precision*, *Recall*, dan *F1-Score* untuk *Content-Based Filtering* dan RMSE untuk *Collaborative Filtering* yang memungkinkan perbandingan objektif dan pemahaman yang jelas terhadap kekuatan dan keterbatasan masing-masing pendekatan. 

Melalui pendekatan *Content-Based Filtering*, sistem mampu memberikan rekomendasi berdasarkan kemiripan penulis dengan memanfaatkan teknik TF-IDF dan *cosine similarity*, yang terbukti sangat efektif terutama dalam kondisi minim interaksi pengguna. Evaluasi menggunakan metrik *Precision*, *Recall*, dan *F1-Score* menunjukkan performa sempurna yang mengindikasikan bahwa model mampu mengenali dan merekomendasikan buku yang relevan secara konsisten. Sementara itu, pendekatan *Collaborative Filtering* melalui model *RecommenderNet* mampu memetakan preferensi pengguna dan buku secara mendalam dengan bantuan embedding. Evaluasi menggunakan RMSE menghasilkan nilai yang rendah yang menunjukkan kemampuan model dalam memberikan saran bacaan yang akurat dan personal berdasarkan interaksi pengguna sebelumnya. Seluruh solusi yang direncanakan—dari analisis eksploratif, pembersihan data, hingga transformasi fitur dan pemilihan algoritma telah terbukti berdampak langsung terhadap peningkatan kualitas rekomendasi. Secara keseluruhan, seluruh solusi yang direncanakan telah berhasil diimplementasikan dengan baik dan memberikan dampak signifikan terhadap performa sistem, baik dari sisi teknis maupun pemenuhan kebutuhan bisnis. Proyek ini menunjukkan bahwa kombinasi pendekatan *Content-Based Filtering* dan *Collaborative Filtering* dapat menjadi strategi efektif dalam membangun sistem rekomendasi buku yang unggul dan bermanfaat secara praktis bagi pengguna.

## References
[1] X. Su and T. M. Khoshgoftaar, "A survey of collaborative filtering techniques," Advances in Artificial Intelligence, vol. 2009, Article ID 421425, 2009.

[2] R. H. Goudar, D. Gm, and R. B. Kaliwal, "Personalized Book Recommendations: A Hybrid Approach Leveraging Collaborative Filtering, Association Rule Mining, and Content-Based Filtering," EAI Endorsed Transactions on Internet of Things, vol. 10, Aug. 2024.

[3] X. He et al., "Neural collaborative filtering," in Proc. 26th Int. Conf. on World Wide Web (WWW), 2017, pp. 173–182. 
