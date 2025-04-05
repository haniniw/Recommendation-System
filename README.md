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

1. **Bagaimana mengembangkan sistem rekomendasi konten musik dan podcast** yang sesuai dengan profil demografis (usia, gender) dan preferensi mendengarkan (genre favorit, waktu mendengarkan, mood) pengguna Spotify?
2. **Bagaimana mengevaluasi performa model rekomendasi** dalam menyajikan konten yang relevan berdasarkan data pengguna tersebut?

---

## 🎯 Goals

Tujuan dari proyek ini dirancang untuk menjawab pertanyaan-pertanyaan di atas, dengan fokus pada:

1. **Mengembangkan sistem rekomendasi yang personal dan relevan:**
   - Memanfaatkan informasi demografis dan perilaku mendengarkan untuk membentuk profil pengguna yang akurat.
   - Menyajikan konten yang sesuai dengan preferensi pengguna.

2. **Mengevaluasi performa model rekomendasi:**
   - Mengukur efektivitas model dengan metrik seperti *Precision* dan *Recall*.
   - Melakukan analisis mendalam terhadap hasil untuk menjamin relevansi dan meningkatkan kepuasan pengguna.

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



# **D. Data Preparation**

Dalam tahap ini, saya menggunakan dua pendekatan untuk membangun sistem rekomendasi berbasis kemiripan: TF-IDF + Cosine Similarity dan Label Encoding + Jaccard Similarity. Keduanya memiliki pendekatan pemrosesan yang berbeda.

**1. TF-IDF + Cosine Similarity**
   
   Tujuan: Mengubah fitur kategorikal menjadi representasi teks untuk dihitung kemiripannya menggunakan TF-IDF dan Cosine Similarity.
  Langkah:
  Menggabungkan semua nilai fitur menjadi satu string per baris (music_feature_text).
  TF-IDF akan memberikan bobot pentingnya tiap kata (fitur) berdasarkan frekuensinya.

**2. Label Encoding + Jaccard Similarity**
   
   Tujuan: Mengubah data kategorikal menjadi format numerik menggunakan LabelEncoder agar dapat dihitung kemiripannya dengan Jaccard Similarity.
    Langkah:
    Setiap nilai unik diubah menjadi angka.
    Hasil encoding digabung dalam music_feature_vector.

📝 Kolom yang digunakan dalam pendekatan untuk rekomendasi musik berdasarkan hasil multivariate analysis:

'Age', 'Gender', 'fav_music_genre', 'music_Influencial_mood', 'music_lis_frequency'

📝 Kolom yang digunakan dalam pendekatan untuk rekomendasi podcast berdasarkan hasil multivariate analysis:

'fav_pod_genre', 'preffered_pod_format'

⚖️ Perbandingan Pendekatan

🔹 TF-IDF + Cosine Similarity

  - Mengubah data kategorikal menjadi teks numerik berbobot.
  - Menggunakan metode Cosine Similarity untuk menghitung kemiripan antar pengguna atau item.
  - Cocok digunakan ketika fitur memiliki banyak variasi atau nilai yang bersifat deskriptif.

Keunggulan: mampu menangkap makna semantik dan tingkat kepentingan fitur antar dokumen.

🔹 Label Encoding + Jaccard Similarity

  - Mengonversi data kategorikal menjadi kode numerik diskrit.
  - Menggunakan Jaccard Similarity untuk membandingkan kemiripan berdasarkan kesamaan nilai.
  - Cocok untuk fitur kategorikal tetap yang tidak memerlukan bobot atau konteks semantik.

Keunggulan: lebih cepat, ringan, dan efisien untuk dataset yang bersifat tabular.


# E. Modelling
## 🎧 Modelling Sistem Rekomendasi Musik & Podcast

Sistem rekomendasi dikembangkan menggunakan dua pendekatan berbeda untuk membandingkan kemiripan pengguna berdasarkan atribut kategorikal.

---

### ✅ 1. Pendekatan TF-IDF + Cosine Similarity

Pendekatan ini menggabungkan fitur-fitur kategorikal (seperti genre musik favorit, mood, usia, dll) menjadi satu teks gabungan per pengguna, lalu dikonversi menjadi vektor numerik berbobot menggunakan TF-IDF.

#### 🔹 Langkah-langkah:
1. **Gabung fitur** menjadi satu string teks per pengguna.
2. **TF-IDF Vectorization**: Mengubah teks menjadi vektor numerik dengan `TfidfVectorizer()`.
3. **Cosine Similarity**: Menghitung tingkat kemiripan antar pengguna berdasarkan arah vektor.
4. **Fungsi Rekomendasi**: Mengembalikan top-N pengguna paling mirip.

---

### ✅ 2. Pendekatan One-Hot Encoding + Jaccard Similarity

Pendekatan ini menggunakan one-hot encoding untuk mengubah data kategorikal menjadi format biner (0/1), lalu menghitung kemiripan berdasarkan seberapa banyak atribut yang sama menggunakan Jaccard similarity.

#### 🔹 Langkah-langkah:
1. **One-Hot Encoding**: Menggunakan `pd.get_dummies()` untuk mengubah kolom kategorikal menjadi format biner.
2. **Jaccard Similarity**: Mengukur kemiripan berdasarkan rasio atribut yang sama terhadap atribut yang berbeda.
3. **Fungsi Rekomendasi**: Mengembalikan top-N pengguna yang paling mirip berdasarkan Jaccard score.
---

### 📊 Perbandingan Kedua Pendekatan

| Aspek                       | TF-IDF + Cosine Similarity        | One-Hot Encoding + Jaccard           |
|-----------------------------|-----------------------------------|--------------------------------------|
| Representasi Data           | Teks vektor berbobot TF-IDF       | Matriks biner (0/1)                  |
| Pengukuran Kemiripan        | Cosine Similarity                 | Jaccard Similarity                   |
| Kecocokan                   | Kombinasi kategorikal kompleks    | Data kategorikal eksplisit           |
| Memperhatikan frekuensi     | ✅ Ya                              | ❌ Tidak                              |
| Interpretasi                | Lebih kontekstual dan fleksibel   | Lebih eksplisit dan langsung         |

---

### 🎯 Kesimpulan

- **TF-IDF + Cosine** menangkap makna dan bobot fitur, cocok untuk kombinasi atribut.
- **One-Hot + Jaccard** lebih simpel dan cepat, cocok jika data sudah eksplisit.
- Pemilihan metode disesuaikan dengan kompleksitas data dan kebutuhan sistem rekomendasi.
---

# F. EVALUASI 






















