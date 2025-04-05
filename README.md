# 🎧 Recommendation System: Model Sistem Rekomendasi Musik dan Podcast pada Aplikasi Spotify

**🧑‍💻 Oleh: Noer Hanifah Suganda**

---

## 📌 Project Overview

Dalam era digital saat ini, sistem rekomendasi telah menjadi komponen penting dalam platform streaming musik seperti **Spotify**. Dengan jumlah konten yang terus berkembang, pengguna kerap merasa kewalahan dalam mencari musik atau podcast yang sesuai dengan selera dan mood mereka. 

Proyek ini bertujuan untuk mengembangkan sistem rekomendasi menggunakan pendekatan **Content-Based Filtering**.

---

## 🎯 Latar Belakang

Beberapa faktor utama yang mendorong pengembangan proyek ini antara lain:

### 1. Pertumbuhan Konten Digital
- Banyaknya jumlah lagu dan podcast yang tersedia di platform streaming menjadikan **pemfilteran konten** sangat penting agar pengguna dapat menemukan konten yang sesuai.

### 2. Personalisasi Mendalam
- Pendekatan **Content-Based Filtering** memungkinkan pembentukan **profil pengguna** yang lebih akurat berdasarkan atribut lagu atau podcast yang disukai, sehingga rekomendasi yang diberikan menjadi lebih **relevan dan personal**.

### 3. Landasan Riset Terkini
- Beberapa studi mendukung penggunaan pendekatan berbasis konten, antara lain:

  > **Chen et al. (2020)** mengusulkan metode pembelajaran representasi audio yang memanfaatkan riwayat mendengarkan pengguna untuk menghasilkan **audio embedding** yang efektif dalam sistem rekomendasi musik berbasis konten.
  
  > **Deldjoo, Schedl, dan Knees (2021)** memberikan tinjauan komprehensif terkait **evolusi dan tantangan sistem rekomendasi musik**, terutama yang berfokus pada integrasi **data sinyal, metadata, dan interaksi pengguna** untuk meningkatkan relevansi rekomendasi.

---

# **B. Business Understanding**

## 🧩 Problem Statements

Berdasarkan latar belakang dan karakteristik dataset Spotify yang berisi informasi demografis serta preferensi mendengarkan, proyek ini difokuskan untuk menjawab dua pertanyaan utama:

1. **Bagaimana mengembangkan sistem rekomendasi konten musik dan podcast**  
3. **Apa metode yang paling baik dalam mengembangkan sistem rekomendasi konten musik dan podcast**
---

## 🎯 Goals

Tujuan dari proyek ini dirancang untuk menjawab pertanyaan-pertanyaan di atas, dengan fokus pada:

1. **Mengembangkan sistem rekomendasi yang personal dan relevan:**
2. **Membandingkan beberapa metode untuk menemukan akurasi terbaik dalam mengembangkan sistem rekomendasi konten musik dan podcast**

---

## 💡 Solution Statement

Untuk menghasilkan sistem rekomendasi yang optimal, pendekatan **Content-Based Filtering** digunakan, disertai evaluasi menggunakan metrik kuantitatif (*Precision*, *Recall*, *F1-Score*) agar solusi dapat dinilai secara objektif.

Terdapat dua pendekatan utama yang digunakan:

### 1. TF-IDF + Cosine Similarity
- Menggabungkan fitur kategori pengguna menjadi string teks.
- Mengubahnya menjadi representasi numerik menggunakan **TF-IDF (Term Frequency-Inverse Document Frequency)**.
- Menggunakan **Cosine Similarity** untuk mengukur kemiripan antar pengguna berdasarkan arah vektor fitur.

### 2. One-hot Encoding + Jaccard Similarity
- Mengubah fitur kategori menjadi representasi biner melalui **One-Hot Encoding**.
- Menggunakan **Jaccard Similarity** untuk mengukur kesamaan antara dua pengguna berdasarkan proporsi atribut yang sama.

---

# **C. Data Understanding**

## 🗃️ EDA - Deskripsi Variabel

**Sumber Dataset:** [Kaggle - Spotify User Behavior Dataset](https://www.kaggle.com/code/arvindkhoda/spotify-user-behavior-dataset)

Dataset terdiri dari **520 baris data** dan **20 kolom**, yang mencakup informasi sebagai berikut:

| No | Kolom                     | Deskripsi                                                                 |
|----|---------------------------|---------------------------------------------------------------------------|
| 1  | Age                       | Kelompok usia pengguna                                                    |
| 2  | Gender                    | Jenis kelamin pengguna                                                    |
| 3  | spotify_usage_period      | Lama penggunaan Spotify                                                   |
| 4  | spotify_listening_device  | Perangkat utama untuk mendengarkan Spotify                                |
| 5  | spotify_subscription_plan | Jenis langganan Spotify                                                   |
| 6  | premium_sub_willingness   | Kesediaan pengguna untuk berlangganan premium                             |
| 7  | preffered_premium_plan    | Paket premium yang diinginkan                                             |
| 8  | preferred_listening_content | Jenis konten yang sering didengarkan (musik/podcast)                    |
| 9  | fav_music_genre           | Genre musik favorit                                                       |
| 10 | music_time_slot           | Waktu favorit mendengarkan musik                                          |
| 11 | music_Influencial_mood    | Mood/situasi yang memengaruhi pilihan musik                               |
| 12 | music_lis_frequency       | Frekuensi mendengarkan musik                                              |
| 13 | music_expl_method         | Cara menemukan musik baru                                                 |
| 14 | music_recc_rating         | Penilaian pengguna terhadap rekomendasi musik Spotify                     |
| 15 | pod_lis_frequency         | Frekuensi mendengarkan podcast                                            |
| 16 | fav_pod_genre             | Genre podcast favorit                                                     |
| 17 | preffered_pod_format      | Format podcast yang lebih disukai                                         |
| 18 | pod_host_preference       | Preferensi terhadap host podcast                                          |
| 19 | preffered_pod_duration    | Durasi podcast yang lebih disukai                                         |
| 20 | pod_variety_satisfaction  | Tingkat kepuasan variasi dan ketersediaan podcast di Spotify             |

---

## 🧹 Kondisi Data

- **Duplikasi:** Terdapat 1 baris duplikat yang telah dihapus.
- **Missing Values:**

| Kolom                    | Jumlah Nilai Hilang |
|--------------------------|---------------------|
| Age                      | 4                   |
| preffered_premium_plan   | 207                 |
| fav_pod_genre            | 147                 |
| preffered_pod_format     | 139                 |
| pod_host_preference      | 140                 |
| preffered_pod_duration   | 128                 |

> Variabel `preffered_premium_plan` dianggap tidak relevan terhadap tujuan model, sehingga tidak diprioritaskan dalam penanganan missing value agar tidak terlalu banyak data yang hilang.

- **Tipe Data:**  
  Sebagian besar kolom bertipe *object* dengan nilai kategori terbatas. Kolom-kolom ini diubah menjadi tipe *category* untuk efisiensi memori dan kemudahan analisis.

- **Outliers:**  
  Tidak dilakukan penanganan outliers karena:
  - Sebagian besar kolom adalah kategorikal.
  - Satu-satunya kolom numerik, `music_recc_rating`, memiliki nilai pada rentang 1–5 dan tetap relevan digunakan untuk evaluasi model rekomendasi.

---

## 📂 Pemisahan Dataset: Musik dan Podcast

Untuk mendukung pengembangan dua sistem rekomendasi yang berbeda (musik dan podcast), dataset dipisah berdasarkan atribut relevan.

### 📀 Dataset Musik

Berisi kolom-kolom yang berkaitan dengan preferensi musik:
![Dataset Musik](https://github.com/user-attachments/assets/110dd753-2518-4154-87de-f9597ea1af11)

### 🎙️ Dataset Podcast

Berisi kolom-kolom yang berkaitan dengan preferensi podcast:
![Dataset Podcast](https://github.com/user-attachments/assets/ccdb045f-6629-4715-a7b8-b0c451645a56)

---

## 🎧 Exploratory Data Analysis – Univariate (Musik)

Visualisasi dan analisis univariat dilakukan pada beberapa atribut utama seperti: *age*, *gender*, *genre musik favorit*, *rating rekomendasi*, dan *frekuensi mendengarkan musik*.

1. **Kelompok Usia Pengguna**
   - Mayoritas pengguna berada pada rentang usia **20–35 tahun** (204 orang).
   - Menunjukkan dominasi pendengar musik dari kalangan dewasa muda.  
   ![Age Distribution](https://github.com/user-attachments/assets/eb2d75ad-5066-486d-9662-1e8357e1d03c)

2. **Distribusi Gender**
   - Sebagian besar pengguna adalah **Perempuan** (190 orang), dibandingkan **Laki-laki** (40) dan **Others** (6).  
   ![Gender Distribution](https://github.com/user-attachments/assets/0ff429e5-fdd2-4bfb-bab7-18f97861b72b)

3. **Mood Pengaruh Musik**
   - Musik paling sering diasosiasikan dengan **relaksasi dan pengurang stres** (92 orang).
   - Disusul oleh kombinasi relaksasi dan motivasi, menunjukkan musik sebagai alat *coping* dan regulasi emosi.

4. **Rating Rekomendasi Musik**
   - Sebagian besar pengguna memberi **rating 3 dan 4** (total 158).
   - Mengindikasikan tingkat kepuasan **sedang hingga tinggi** terhadap rekomendasi Spotify.  
   ![Rating Musik](https://github.com/user-attachments/assets/2861b722-c0ca-4e3e-9048-b266560ae031)

5. **Genre Musik Favorit**
   - Genre paling disukai adalah **Melody** (139 orang), disusul **Pop** dan **Classical**.
   - Genre seperti **Rock** dan **Kpop** kurang populer.  
   ![Genre Musik](https://github.com/user-attachments/assets/8f5bcfbe-0856-4f36-b370-de9f8cd81d2f)

6. **Konteks Mendengarkan Musik**
   - Umumnya musik didengarkan saat **bepergian** dan di waktu **luang**.  
   ![Situasi Musik](https://github.com/user-attachments/assets/3623e4ae-6b9a-4b08-890f-7437fa70c6f5)

---

## 🎙️ Exploratory Data Analysis – Univariate (Podcast)

Analisis dilakukan pada atribut usia, gender, genre podcast favorit, format podcast favorit, dan tingkat kepuasan variasi podcast.

1. **Kelompok Usia**
   - Pengguna podcast mayoritas juga berusia **20–35 tahun** (61 pengguna).
   - Jumlah lebih sedikit karena ukuran dataset podcast lebih kecil.  
   ![Podcast Age](https://github.com/user-attachments/assets/b158b36f-674d-460a-98f8-f2d38f78832c)

2. **Distribusi Gender**
   - Mayoritas pengguna adalah **Perempuan** (80 orang), dibandingkan **Laki-laki** (18) dan **Others** (6).  
   ![Podcast Gender](https://github.com/user-attachments/assets/8f91ad54-1a89-4fb9-ae20-e4cf4a29fa4e)

3. **Genre Podcast Favorit**
   - Didominasi oleh **Health and Fitness** (41), **Lifestyle and Health** (25), dan **Sports** (23).  
   ![Podcast Genre](https://github.com/user-attachments/assets/a8c9ba4c-20d0-47e3-984f-d8ec13b8c91a)

4. **Format Podcast Favorit**
   - Disukai format **Storytelling** (44) dan **Interview** (36).
   - Menunjukkan preferensi terhadap konten naratif dan interaktif.  
   ![Podcast Format](https://github.com/user-attachments/assets/67cb7772-031d-4629-a03a-22216b584e9f)

---

## 📊 Multivariate EDA – Musik

### 1. Hubungan Genre Musik dan Rating Rekomendasi
![ANOVA Genre vs Rating](https://github.com/user-attachments/assets/ac75ad12-04ff-4d1c-be7b-cad87e198c47)

- **p-value = 0.000583 (< 0.05)** → Perbedaan rating antar genre signifikan secara statistik.
- **F-statistic = 3.83** → Variabilitas antar genre cukup besar.
- **Kesimpulan:** Genre musik berpengaruh terhadap rating rekomendasi musik.

---

### 2. Hubungan Mood dan Genre Musik
![Chi-square Mood vs Genre](https://github.com/user-attachments/assets/34909cb2-5b6e-495e-a036-c84611a68b04)

- **Chi-square = 142.76**, **p-value = 0.00043**
- **Kesimpulan:** Ada hubungan signifikan antara mood dan genre musik.

---

### 3. Hasil Uji Lainnya:

- **Age vs Genre Musik**
  - Chi-Square = 15.77, p-value = 0.327
  - ❌ Tidak ada hubungan signifikan.

- **Gender vs Genre Musik**
  - Chi-Square = 32.56, p-value = 0.003
  - ✅ Terdapat hubungan signifikan.

- **Age vs Mood Musik**
  - Chi-Square = 39.60, p-value = 0.043
  - ✅ Terdapat hubungan signifikan.

- **Age vs Gender**
  - Chi-Square = 8.12, p-value = 0.087
  - ❌ Tidak ada hubungan signifikan.

---

## 🎧 Multivariate EDA – Podcast

### 1. Hubungan Genre Podcast dan Format
![Chi Podcast Genre vs Format](https://github.com/user-attachments/assets/cda246fa-1941-4c44-b8b7-400a8fe005ac)

- **Chi-square = 25.81**, **p-value = 0.039**
- ✅ Ada hubungan signifikan antara genre dan format podcast.

### 2. Durasi Podcast dan Frekuensi Mendengarkan
![ANOVA Durasi vs Frekuensi](https://github.com/user-attachments/assets/2d4a2f83-34d3-4c50-b742-46862dda39a1)

- **p-value = 0.176 (> 0.05)** → Tidak ada hubungan signifikan.
- **Kesimpulan:** Durasi podcast tidak terlalu memengaruhi frekuensi mendengarkan.

### 3. Hasil Uji Lainnya:
- **Genre Podcast vs Frekuensi Mendengarkan**
  - ANOVA (p = 0.3616), Kruskal-Wallis (p = 0.5042)
  - ❌ Tidak ada hubungan signifikan.

- **Host Podcast vs Genre Podcast**
  - Chi-Square = 14.34, p-value = 0.1580
  - ❌ Tidak ada hubungan signifikan.

- **Host Podcast vs Format Podcast**
  - Chi-Square = 8.34, p-value = 0.2140
  - ❌ Tidak ada hubungan signifikan.

- **Host Podcast vs Kepuasaan Skor**
  - Chi-Square = 11.04, p-value = 0.1995
  - ❌ Tidak ada hubungan signifikan.

# **D. Data Preparation**

Dalam tahap ini, digunakan dua pendekatan utama untuk membangun sistem rekomendasi berbasis kemiripan: **TF-IDF + Cosine Similarity** dan **Label Encoding + Jaccard Similarity**. Keduanya memiliki metode pemrosesan yang berbeda namun saling melengkapi.

---

## 🎵 1. Data Preparation untuk Musik

### a. Pemilihan Fitur
Dipilih fitur-fitur yang relevan untuk merepresentasikan profil pengguna dan preferensi musiknya:

- `genre_music`
- `mood_music`
- `listening_time_music`
- `age_group`
- `gender`
- `music_rating` *(digunakan sebagai target evaluasi)*

### b. Label Encoding
Seluruh fitur kategorikal dikonversi menjadi representasi numerik agar dapat digunakan dalam perhitungan Jaccard.

### c. Perhitungan Jaccard Similarity
Menggunakan library `scipy` untuk menghitung **Jaccard Distance**, lalu dikonversi menjadi **Jaccard Similarity** antar pengguna.

---

## 🎙️ 2. Data Preparation untuk Podcast

### a. Pemilihan Fitur
Fitur yang dipilih mencerminkan kepuasan pengguna terhadap konten podcast:

- `genre_podcast`
- `mood_podcast`
- `listening_time_podcast`
- `age_group`
- `gender`
- `pod_variety_satisfaction` *(target evaluasi)*

### b. Mapping Skor Kepuasan
Nilai kategorikal pada `pod_variety_satisfaction` diubah menjadi angka untuk keperluan analisis.

### c. Label Encoding
Seluruh fitur dikodekan ke bentuk numerik sama seperti pada data musik.

### d. Perhitungan Jaccard Similarity
Menggunakan pendekatan yang sama dengan data musik untuk menghitung kemiripan antar pengguna podcast.

---

# **E. Modelling**

## 🎧 Modelling Sistem Rekomendasi Musik & Podcast

Sistem rekomendasi dikembangkan menggunakan tiga pendekatan untuk membandingkan kemiripan antar pengguna berdasarkan atribut kategorikal.

---

### ✅ 1. TF-IDF + Cosine Similarity

Menggabungkan fitur kategorikal menjadi satu representasi teks yang kemudian diolah menggunakan TF-IDF untuk menangkap bobot kata, dan Cosine Similarity untuk mengukur kemiripan antar pengguna.

#### 🔹 Langkah-langkah:
1. **Gabungkan fitur** menjadi string teks per pengguna.
2. **TF-IDF Vectorization** menggunakan `TfidfVectorizer()`.
3. **Cosine Similarity**: Mengukur arah vektor antar pengguna.
4. **Fungsi**: `get_recommendations_tfidf(index)` untuk top-N rekomendasi pengguna mirip.

---

### ✅ 2. One-Hot Encoding + Jaccard Similarity

Mengubah fitur kategorikal menjadi bentuk biner (0/1) lalu menghitung kemiripan berdasarkan proporsi atribut yang sama antar pengguna.

#### 🔹 Langkah-langkah:
1. **One-Hot Encoding** menggunakan `pd.get_dummies()`.
2. **Jaccard Similarity**: Mengukur rasio atribut sama dibandingkan gabungan atribut berbeda.
3. **Fungsi**:
   - `get_music_recommendations_jaccard(index)`
   - `get_podcast_recommendations_jaccard(index)`

---

### ✅ 3. Hybrid Model (TF-IDF + Jaccard Similarity)

Menggabungkan hasil kemiripan dari pendekatan TF-IDF dan Jaccard untuk menciptakan sistem rekomendasi yang lebih stabil dan adaptif.

#### 🎯 Tujuan:
Mengintegrasikan semantic-based TF-IDF dan struktur set-based Jaccard untuk meningkatkan akurasi rekomendasi.

#### ⚙️ Langkah-Langkah:
1. Hitung skor kemiripan dari:
   - **TF-IDF (Cosine Similarity)**
   - **Jaccard Similarity**
2. Gabungkan kedua skor menggunakan rata-rata sederhana.
3. **Fungsi**: `get_hybrid_recommendations(index)`

---

## 📊 Perbandingan Pendekatan

| **Aspek**                   | **TF-IDF + Cosine**                | **One-Hot + Jaccard**               |
|-----------------------------|------------------------------------|-------------------------------------|
| Representasi Data           | Teks vektor berbobot (TF-IDF)      | Matriks biner (0/1)                 |
| Pengukuran Kemiripan        | Cosine Similarity                  | Jaccard Similarity                  |
| Kecocokan Data              | Atribut kombinasi dan fleksibel    | Data kategorikal eksplisit          |
| Memperhatikan Frekuensi     | ✅ Ya                               | ❌ Tidak                             |
| Interpretasi                | Kontekstual dan fleksibel          | Eksplisit dan mudah dipahami        |

---

### 📌 Ringkasan Fungsi Rekomendasi

| **Nama Fungsi**                           | **Deskripsi**                                      |
|-------------------------------------------|---------------------------------------------------|
| `get_recommendations_tfidf(index)`        | Rekomendasi berdasarkan TF-IDF + Cosine Similarity |
| `get_music_recommendations_jaccard(index)`| Rekomendasi musik berbasis Jaccard Similarity      |
| `get_podcast_recommendations_jaccard(index)`| Rekomendasi podcast berbasis Jaccard Similarity  |
| `get_hybrid_recommendations(index)`       | Rekomendasi gabungan TF-IDF dan Jaccard            |


# F. Evaluasi

Pada tahap evaluasi ini, digunakan beberapa metrik untuk mengukur performa sistem rekomendasi, yaitu:

---

### 🎯 1. Precision  
**Definisi:**  
Proporsi item yang direkomendasikan dan memang relevan dari semua item yang direkomendasikan.

**Interpretasi:**  
Semakin tinggi precision, semakin *akurat* sistem dalam memberikan rekomendasi yang sesuai selera pengguna.

---

### 🎯 2. Recall  
**Definisi:**  
Proporsi item relevan yang berhasil terambil oleh sistem dari semua item relevan yang tersedia.

**Interpretasi:**  
Semakin tinggi recall, semakin *lengkap* sistem dalam menangkap item yang disukai pengguna.

---

### 🎯 3. F1-Score  
**Definisi:**  
Gabungan dari precision dan recall dalam satu metrik (menggunakan rata-rata harmonis).

**Interpretasi:**  
Metrik ini mengukur keseimbangan antara *akurasi* dan *cakupan* sistem rekomendasi.

---

### 🎯 4. Rata-rata Selisih Rating Rekomendasi  
**Definisi:**  
Mengukur perbedaan antara rating awal (sebelum rekomendasi) dengan rating dari item yang direkomendasikan.

**Interpretasi Nilai:**
- Nilai **negatif** → Rekomendasi cenderung lebih rendah dari preferensi awal.  
- Nilai **mendekati 0** → Rekomendasi cenderung sesuai dengan preferensi awal.  
- Nilai **positif** → Rekomendasi cenderung lebih tinggi (jarang terjadi).

---

### 🎯 5. Rata-rata Proporsi Rekomendasi dengan Rating Lebih Baik/Sama  
**Definisi:**  
Mengukur persentase rekomendasi yang memiliki rating sama atau lebih tinggi dibanding item yang disukai pengguna sebelumnya.

**Interpretasi Nilai:**
- Semakin tinggi nilai (mendekati 100%), sistem semakin *relevan dan aman*.  
- Jika proporsi rendah, banyak rekomendasi tidak sesuai preferensi pengguna.

---

![image](https://github.com/user-attachments/assets/d4fb989d-31b1-43bc-9a77-f9b09057d5d3)

## 🔍 1. TF-IDF vs Jaccard vs Hybrid – Musik  
### 📈 Evaluasi Umum:
![image](https://github.com/user-attachments/assets/8e357346-b95c-4405-acd8-ae6ceedfad79)

- Semua metode memberikan rekomendasi yang relevan (Precision = 1.00 dan proporsi lebih baik/sama = 100%).

---

## 🔍 2. TF-IDF vs Jaccard vs Hybrid – Podcast  
### 📈 Evaluasi Umum:
![image](https://github.com/user-attachments/assets/a965ca5d-60c9-49ec-a92d-f69e3b65ec76)

- Semua metode menunjukkan performa tinggi (Precision = 1.00, Proporsi ≥ 100%).  
- **Hybrid** menunjukkan keunggulan karena:
  - Rata-rata selisih skor paling kecil.
  - Recall dan F1-Score paling tinggi (meski selisihnya kecil).

---

## 🎯 Goal 1: Mengembangkan Sistem Rekomendasi yang Personal dan Relevan

Sistem rekomendasi berhasil dikembangkan melalui pendekatan berikut:
- **TF-IDF + Cosine Similarity**: cocok untuk konten berbasis teks.
- **Label Encoding + Jaccard Similarity**: efektif untuk fitur kategorikal.
- **Hybrid (TF-IDF + Jaccard)**: menggabungkan keunggulan dari keduanya.

Sistem mampu merekomendasikan konten dengan rating yang sama atau lebih tinggi dari preferensi awal pengguna (≥ 60%).  
Precision tinggi (1.00) menunjukkan sistem mampu menghindari rekomendasi yang tidak relevan.

---

## 🎯 Goal 2: Membandingkan Metode untuk Menemukan Akurasi Terbaik

- **Hybrid (TF-IDF + Jaccard)** terbukti sebagai metode paling unggul untuk **podcast**.  
- Untuk **musik**, hybrid juga menunjukkan performa lebih baik:
  - Rata-rata selisih rating lebih kecil (-0.155).
  - Namun, F1-Score masih setara dengan metode lain (0.69).

# Reference

Deldjoo, Y., Schedl, M., & Knees, P. (2021). Content-driven Music Recommendation: Evolution, State of the Art, and Challenges [Preprint].

Chen, K., Liang, B., Ma, X., & Gu, M. (2020). Learning Audio Embeddings with User Listening Data for Content-based Music Recommendation [Preprint].
