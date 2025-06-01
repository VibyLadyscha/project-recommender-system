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
1. Mengembangkan sistem rekomendasi buku yang memanfaatkan pendekatan Content-Based Filtering dan Collaborative Filtering untuk memberikan saran bacaan yang personal dan kontekstual.
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
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

## References
[1] X. Su and T. M. Khoshgoftaar, "A survey of collaborative filtering techniques," Advances in Artificial Intelligence, vol. 2009, Article ID 421425, 2009.

[2] R. H. Goudar, D. Gm, and R. B. Kaliwal, "Personalized Book Recommendations: A Hybrid Approach Leveraging Collaborative Filtering, Association Rule Mining, and Content-Based Filtering," EAI Endorsed Transactions on Internet of Things, vol. 10, Aug. 2024.

[3] X. He et al., "Neural collaborative filtering," in Proc. 26th Int. Conf. on World Wide Web (WWW), 2017, pp. 173–182. 

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
