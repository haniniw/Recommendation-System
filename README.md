# Recommendation System: Model Sistem Rekomendasi Musik dan Podcast pada Aplikasi Spotify
Oleh: Noer Hanifah Suganda
---
**Project Overview**

Dalam era digital saat ini, sistem rekomendasi telah menjadi komponen penting dalam platform streaming musik seperti Spotify. Dengan jumlah konten yang terus berkembang, pengguna kerap merasa kewalahan dalam mencari musik atau podcast yang sesuai dengan selera dan mood mereka. Proyek ini bertujuan untuk mengembangkan sistem rekomendasi menggunakan pendekatan Content-Based Filtering.

Latar belakang proyek ini didorong oleh beberapa faktor:

*   Pertumbuhan Konten Digital: Dengan banyaknya lagu dan podcast yang tersedia, dibutuhkan sistem yang mampu menyaring dan menyesuaikan rekomendasi dengan kebutuhan individu.

- Personalisasi Mendalam: Pendekatan content-based filtering memungkinkan pembuatan profil pengguna yang akurat berdasarkan atribut lagu, sehingga rekomendasi yang dihasilkan lebih relevan dan personal.

- Landasan Riset Terkini:

  Beberapa studi terkini mendukung pendekatan ini. Misalnya, Chen et al. (2020) mengusulkan metode pembelajaran representasi audio yang memanfaatkan data riwayat mendengarkan untuk menghasilkan audio embedding yang efektif dalam sistem rekomendasi musik berbasis konten.
  
  Selain itu, survei oleh Deldjoo, Schedl, dan Knees (2021) memberikan tinjauan mendalam mengenai evolusi dan tantangan dalam sistem rekomendasi musik yang didorong oleh konten, dengan fokus pada integrasi data sinyal, metadata, dan konten pengguna untuk meningkatkan rekomendasi.

# **B. Business Understanding**

**Problem Statements**

Berdasarkan uraian latar belakang dan karakteristik dataset Spotify yang berisi informasi demografis dan preferensi mendengarkan, rumusan masalah yang akan dijawab dalam proyek ini adalah sebagai berikut:

1.   Bagaimana mengembangkan sistem rekomendasi konten musik dan podcast yang sesuai dengan profil demografis (usia, gender) dan preferensi mendengarkan (genre favorit, waktu mendengarkan, mood) pengguna Spotify
2. Bagaimana mengevaluasi performa model rekomendasi dalam menyajikan konten yang relevan berdasarkan data demografis dan preferensi mendengarkan pengguna Spotify?

**Goals**

Berdasarkan rumusan masalah tersebut, tujuan dari proyek penelitian ini adalah:

1. Mengembangkan sistem rekomendasi konten musik dan podcast yang personal dan relevan:
Mengetahui cara memanfaatkan informasi demografis dan perilaku mendengarkan untuk membangun profil pengguna yang akurat sehingga dapat menyajikan rekomendasi yang sesuai.

2. Mengevaluasi performa model rekomendasi:
Mengukur efektivitas sistem rekomendasi yang dibangun melalui metrik evaluasi yang tepat (misalnya, Precisiondan  Recall), serta melakukan analisis mendalam terhadap hasil yang diperoleh untuk memastikan relevansi dan kepuasan pengguna.

**Solution Statement**

Untuk mengembangkan sistem rekomendasi konten musik dan podcast yang personal dan relevan, saya menggunakan pendekatan Content-Based Filtering dengan evaluasi metrik terukur (Precision, F-1 score, dan Recall) sehingga solusi yang dihasilkan dapat dinilai secara objektif.

1. TF-IDF + Cosine Similarity 
Pada pendekatan pertama, fitur kategori pengguna dikombinasikan menjadi teks dan diubah menjadi representasi numerik menggunakan TF-IDF (Term Frequency-Inverse Document Frequency).
Kemudian, cosine similarity digunakan untuk mengukur kemiripan antara pengguna berdasarkan arah vektor fitur mereka.

2. One-hot Encoding + Jaccard Similarity
Pada pendekatan kedua, fitur kategorikal yang telah  diubah menjadi representasi biner menggunakan one-hot encoding, digunakan Jaccard similarity untuk mengukur seberapa mirip dua pengguna berdasarkan proporsi atribut yang sama dari total atribut unik.

# **C. Data Understanding**

**EDA - Deskripsi Variabel**
Sumber: https://www.kaggle.com/code/arvindkhoda/spotify-user-behavior-dataset

Dataset ini memiliki 520 baris data dan 20 kolom. Berikut adalah deskripsi masing-masing kolom:

Age – Kelompok usia pengguna.

Gender – Jenis kelamin pengguna.

spotify_usage_period – Lama waktu penggunaan Spotify.

spotify_listening_device – Perangkat utama yang digunakan untuk mendengarkan Spotify.

spotify_subscription_plan – Jenis paket langganan Spotify yang digunakan.

premium_sub_willingness – Kesediaan pengguna untuk berlangganan premium.

preffered_premium_plan – Paket premium yang diinginkan pengguna (jika ada).

preferred_listening_content – Jenis konten utama yang sering didengarkan (musik/podcast).

fav_music_genre – Genre musik favorit pengguna.

music_time_slot – Waktu favorit untuk mendengarkan musik.

music_Influencial_mood – Mood atau situasi yang memengaruhi pilihan musik.

music_lis_frequency – Frekuensi mendengarkan musik.

music_expl_method – Cara pengguna menemukan musik baru.

music_recc_rating – Penilaian pengguna terhadap rekomendasi musik dari Spotify.

pod_lis_frequency – Frekuensi mendengarkan podcast.

fav_pod_genre – Genre podcast favorit pengguna.

preffered_pod_format – Format podcast yang lebih disukai.

pod_host_preference – Preferensi pengguna terhadap host podcast (terkenal atau tidak).

preffered_pod_duration – Durasi podcast yang lebih disukai (pendek atau panjang).

pod_variety_satisfaction – Tingkat kepuasan terhadap variasi dan ketersediaan podcast di Spotify

**Kondisi Data**

Duplikasi: Terdapat 1 baris duplikat yang dihapus.
Missing Values: 
Age: Terdapat 4 nilai yang hilang.

preffered_premium_plan: Terdapat 207 nilai yang hilang.

fav_pod_genre: Terdapat 147 nilai yang hilang.

preffered_pod_format: Terdapat 139 nilai yang hilang.

pod_host_preference: Terdapat 140 nilai yang hilang.

preffered_pod_duration: Terdapat 128 nilai yang hilang.

Karena terdapat baris yang hilang terlalu banyak, dan tidak semua variabel akan digunakan, maka saya tidak akan menghapus missing values dari variabel preffered_premium_plan yang tidak relevan dalam menjawab goals agar data yang berkurang tidak terlalu banyak.

Tipe Data: Sebagian besar kolom bertipe object yang mengandung nilai kategorikal dengan jumlah kategori yang terbatas, saya mengubahnya ke tipe data category guna meningkatkan efisiensi memori dan mempermudah analisis.

Outliers: Tidak dilakukan penanganan outliers karena tipe data kategorik dan kolom numerik hanya satu, yaitu music_recc_rating yang hanya direntang 1-5 berguna untuk kebutuhan sistem rekomendasi data.

**Membagi Dataset Rekomendasi Musik dan Rekomendasi Podcast**

Sesuai dengan goals untuk mengembangkan rekomendasi musik dan podcast, dataset dibuat secara terpisah dengan masing-masing isi kolom yang relevan berdasarkan kebutuhan.
Berikut adalah kolom-kolom yang digunakan pada masing-masing dataset
![image](https://github.com/user-attachments/assets/6c445560-e3c5-44b4-9876-9c5776459877)

![image](https://github.com/user-attachments/assets/3dbd665f-0afb-49fc-8105-09f7ef8055f4)

**Exploratory Data Analysis (EDA) Musik**

Visualisasi & Analisis Univariate pada atribut age, gender, genre musik favorit, rating rekomendasi:

![image](https://github.com/user-attachments/assets/5aa64e69-9f2e-4e42-ada1-e624eb7f9501)

![image](https://github.com/user-attachments/assets/b0c49180-d025-4439-9003-44ae462bc9aa)

**Exploratory Data Analysis (EDA) Podcast**

Visualisasi & Analisis Univariate pada atribut age, gender, genre podcast favorit, format podcast favorit, dan rating kepuasan variasi podcast:

![image](https://github.com/user-attachments/assets/7c0db44c-70cb-4ebd-957f-91a10aaeccbf)

![image](https://github.com/user-attachments/assets/5a0125b9-e341-497d-afb6-efab79da5c34)

![image](https://github.com/user-attachments/assets/68c4ebec-c3d6-4aed-87cb-1b42fb6809a9)

**Multivariate EDA Music**

![image](https://github.com/user-attachments/assets/ac75ad12-04ff-4d1c-be7b-cad87e198c47)

![image](https://github.com/user-attachments/assets/34909cb2-5b6e-495e-a036-c84611a68b04)

**Multivariate EDA Podcast**

![image](https://github.com/user-attachments/assets/2d4a2f83-34d3-4c50-b742-46862dda39a1)

