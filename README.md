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
   - Analisis Eksploratif dilakukan untuk menjelajahi dataset untuk memahami struktur data, distribusi rating, popularitas buku, dan karakteristik pengguna.
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
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

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


#### Interpretasi Hasil

![evaluasi-cf](https://raw.githubusercontent.com/VibyLadyscha/project-recommender-system/main/img/collaborative%20filtering_rmse.png)

Setelah melakukan pelatihan model *Collaborative Filtering*, dapat dilihat bahwa plot metrik RMSE yang menunjukkan kinerja model dalam bentuk grafik. Dari plot tersebut, model menghasilkan nilai RMSE sebesar 0.2915 pada train dan 0.3136 pada validation. Angka ini menunjukkan bahwa kinerja model sudah cukup baik karena nilai RMSE yang lebih rendah menunjukkan kesalahan yang lebih kecil dalam prediksi.

## References
[1] X. Su and T. M. Khoshgoftaar, "A survey of collaborative filtering techniques," Advances in Artificial Intelligence, vol. 2009, Article ID 421425, 2009.

[2] R. H. Goudar, D. Gm, and R. B. Kaliwal, "Personalized Book Recommendations: A Hybrid Approach Leveraging Collaborative Filtering, Association Rule Mining, and Content-Based Filtering," EAI Endorsed Transactions on Internet of Things, vol. 10, Aug. 2024.

[3] X. He et al., "Neural collaborative filtering," in Proc. 26th Int. Conf. on World Wide Web (WWW), 2017, pp. 173–182. 

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
