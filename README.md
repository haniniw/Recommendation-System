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

1. Age – Kelompok usia pengguna.
2. Gender – Jenis kelamin pengguna.
3. spotify_usage_period – Lama waktu penggunaan Spotify.
4. spotify_listening_device – Perangkat utama yang digunakan untuk mendengarkan Spotify.
5. spotify_subscription_plan – Jenis paket langganan Spotify yang digunakan.
6. premium_sub_willingness – Kesediaan pengguna untuk berlangganan premium.
7. preffered_premium_plan – Paket premium yang diinginkan pengguna (jika ada).
8. preferred_listening_content – Jenis konten utama yang sering didengarkan (musik/podcast).
9. fav_music_genre – Genre musik favorit pengguna.
10. music_time_slot – Waktu favorit untuk mendengarkan musik.
11. music_Influencial_mood – Mood atau situasi yang memengaruhi pilihan musik.
12. music_lis_frequency – Frekuensi mendengarkan musik.
13. music_expl_method – Cara pengguna menemukan musik baru.
14. music_recc_rating – Penilaian pengguna terhadap rekomendasi musik dari Spotify.
15. pod_lis_frequency – Frekuensi mendengarkan podcast.
16. fav_pod_genre – Genre podcast favorit pengguna.
17. preffered_pod_format – Format podcast yang lebih disukai.
18. pod_host_preference – Preferensi pengguna terhadap host podcast (terkenal atau tidak).
19. preffered_pod_duration – Durasi podcast yang lebih disukai (pendek atau panjang).
20. pod_variety_satisfaction – Tingkat kepuasan terhadap variasi dan ketersediaan podcast di Spotify

**Kondisi Data**

- **Duplikasi:** Terdapat 1 baris duplikat yang dihapus.
- **Missing Values:** 
  - Age: Terdapat 4 nilai yang hilang.
  - preffered_premium_plan: Terdapat 207 nilai yang hilang.
  - fav_pod_genre: Terdapat 147 nilai yang hilang.
  - preffered_pod_format: Terdapat 139 nilai yang hilang.
  - pod_host_preference: Terdapat 140 nilai yang hilang.
  - preffered_pod_duration: Terdapat 128 nilai yang hilang.

  Karena baris yang mempunyai missing value terlalu banyak, dan tidak semua variabel akan digunakan, maka saya tidak akan menghapus missing values dari variabel preffered_premium_plan yang tidak relevan dalam menjawab goals agar data yang berkurang tidak terlalu banyak.

- **Tipe Data:** Sebagian besar kolom bertipe object yang mengandung nilai kategorikal dengan jumlah kategori yang terbatas, saya mengubahnya ke tipe data category supaya meningkatkan efisiensi memori dan mempermudah analisis.

- **Outliers:** Tidak dilakukan penanganan outliers karena tipe data kategorik dan kolom numerik hanya satu, yaitu music_recc_rating yang hanya direntang 1-5 akan berguna untuk kebutuhan sistem rekomendasi data.

**Membagi Dataset Rekomendasi Musik dan Rekomendasi Podcast**

Sesuai dengan goals untuk mengembangkan rekomendasi musik dan podcast, dataset dibuat secara terpisah dengan masing-masing isi kolom yang relevan berdasarkan kebutuhan.

Berikut adalah kolom-kolom yang digunakan pada masing-masing dataset

**Dataset musik**
![image](https://github.com/user-attachments/assets/110dd753-2518-4154-87de-f9597ea1af11)


**Dataset podcast**
![image](https://github.com/user-attachments/assets/ccdb045f-6629-4715-a7b8-b0c451645a56)


**Exploratory Data Analysis Univariate Musik**

Visualisasi & Analisis Univariate pada atribut age, gender, genre musik favorit, rating rekomendasi, dan frekuensi mendengarkan:

1. Mayoritas pengguna berada pada rentang usia produktif 20–35 tahun (204 orang), menunjukkan dominasi pendengar musik dari kalangan dewasa muda.
![image](https://github.com/user-attachments/assets/eb2d75ad-5066-486d-9662-1e8357e1d03c)

2. Sebagian besar pengguna adalah perempuan (190 orang), jauh lebih banyak dibanding laki-laki (40) dan lainnya (6)
![image](https://github.com/user-attachments/assets/0ff429e5-fdd2-4bfb-bab7-18f97861b72b)

3. Musik paling sering diasosiasikan dengan relaksasi dan pengurang stres (92 orang), diikuti oleh kombinasi relaksasi dan motivasi. Ini menandakan musik dipakai sebagai alat coping dan regulasi emosi.

4. Sebagian besar pengguna memberikan rating 3 dan 4 (total 158), yang menunjukkan tingkat kepuasan sedang hingga tinggi terhadap rekomendasi musik.
![image](https://github.com/user-attachments/assets/2861b722-c0ca-4e3e-9048-b266560ae031)

5. Genre paling disukai adalah Melody (139 orang), diikuti Pop dan Classical. Genre seperti Rock dan Kpop kurang populer dalam dataset ini.
![image](https://github.com/user-attachments/assets/8f5bcfbe-0856-4f36-b370-de9f8cd81d2f)

6. Konteks paling umum untuk mendengarkan musik adalah saat bepergian dan waktu luang, baik secara tunggal maupun kombinasi keduanya. 
![image](https://github.com/user-attachments/assets/3623e4ae-6b9a-4b08-890f-7437fa70c6f5)

   
**Exploratory Data Analysis Univariate Podcast**

Visualisasi & Analisis Univariate pada atribut age, gender, genre podcast favorit, format podcast favorit, dan rating kepuasan variasi podcast:

1. Pengguna podcast juga sama seperti pengguna musik berada di mayoritas kelompok usia 20-35 walaupun jumlahnya lebih sedikit hanya 61 pengguna. Hal ini dipengaruhi oleh dataset podcast yang lebih sedikit dibandingkan dengan dataset musik.
![image](https://github.com/user-attachments/assets/b158b36f-674d-460a-98f8-f2d38f78832c)

3. Mayoritas pengguna podcast juga adalah Female (80) dibandingkan dengan Male (18) dan Others (6).
![image](https://github.com/user-attachments/assets/8f91ad54-1a89-4fb9-ae20-e4cf4a29fa4e)

4. Genre podcast favorit didominasi oleh Health and Fitness (41), Lifestyle and Health (25), dan Sports (23).
![image](https://github.com/user-attachments/assets/a8c9ba4c-20d0-47e3-984f-d8ec13b8c91a)

5. Format podcast yang disukai adalah Story telling (44) dan Interview (36), yang menunjukkan preferensi terhadap konten naratif dan interaksi dengan narasumber.
![image](https://github.com/user-attachments/assets/67cb7772-031d-4629-a03a-22216b584e9f)


**Multivariate EDA Music**

![image](https://github.com/user-attachments/assets/ac75ad12-04ff-4d1c-be7b-cad87e198c47)
Saya melakukan uji anova untuk melihat hubungan antara variabel rating musik dengan genre musik. Hasilnya diperoleh sebagai berikut:

**p-value = 0.000583 (kurang dari 0.05)** menunjukkan bahwa perbedaan rata-rata music_recc_rating antar genre musik (fav_music_genre) adalah signifikan secara statistik.

**F-statistic = 3.83** mengindikasikan bahwa variabilitas antara kelompok genre musik lebih besar dibandingkan dengan variabilitas dalam kelompok.

**Kesimpulan:** Genre musik memiliki pengaruh signifikan terhadap rating rekomendasi musik. 

![image](https://github.com/user-attachments/assets/34909cb2-5b6e-495e-a036-c84611a68b04)
Saya melakukan uji chi-square untuk melihat hubungan antara variabel mood dan genre musik. Hasilnya diperoleh sebagai berikut:

**Chi-square statistic: 142.76147694959033
p-value: 0.00043244726600508274**
Ada hubungan signifikan antara mood dan genre musik.

**Hasil uji analisis variabel lainnya:**

**- Hubungan antara Age dan fav_music_genre**

  **- Nilai Chi-Square = 15.774, p-value = 0.327**

  **Kesimpulan:** Tidak terdapat hubungan yang signifikan antara kelompok usia dan genre musik favorit (karena p-value > 0.05). Ini menunjukkan bahwa preferensi genre musik cenderung tidak dipengaruhi oleh perbedaan usia dalam data ini.

**- Hubungan antara Gender dan fav_music_genre**

  **- Nilai Chi-Square = 32.560, p-value = 0.003**

  **- Kesimpulan:** Terdapat hubungan yang signifikan antara jenis kelamin dan genre musik favorit (karena p-value < 0.05). Hal ini mengindikasikan bahwa preferensi genre musik cenderung bervariasi antar gender, dengan distribusi genre tertentu lebih dominan pada gender tertentu.

**- Hubungan antara Age dan music_Influencial_mood**

  **- Nilai Chi-Square = 39.603, p-value = 0.043**

  **- Kesimpulan:** Terdapat hubungan yang signifikan antara kelompok usia dan suasana hati atau alasan emosional yang memengaruhi seseorang dalam mendengarkan musik. Artinya, motivasi emosional dalam mendengarkan musik (seperti relaksasi, motivasi, atau kesedihan) cenderung berbeda antar kelompok usia.

**- Hubungan antara Age dan Gender**

  **- Nilai Chi-Square = 8.120, p-value = 0.087**

  **- Kesimpulan:** Tidak terdapat hubungan yang signifikan antara kelompok usia dan gender. 


**Multivariate EDA Podcast**

![image](https://github.com/user-attachments/assets/cda246fa-1941-4c44-b8b7-400a8fe005ac)
Saya melakukan uji ch-square untuk melihat hubungan antara variabel genre dengan format podcast. Hasilnya diperoleh sebagai berikut:

**Chi-square statistic: 25.81665230286194**
**p-value: 0.039994571314622494**
✅ Dapat disimpulkan ada hubungan yang signifikan antara Genre dan Format Podcast. Analisis ini saya jadikan acuan untuk menentukan atribut yang relevan untuk mengembangkan rekomendasi podcast.

![image](https://github.com/user-attachments/assets/2d4a2f83-34d3-4c50-b742-46862dda39a1)
Saya melakukan analisis dengan atribut lainnya juga, salah satunya adalah atribut preferred podcast duration dengan listening frequency. Seperti penjelasan di bawah ini, hubungan antara kedua atribut tersebut kurang relevan.

Dari hasil ANOVA, nilai **p-value (PR(>F)) = 0.176351** menunjukkan bahwa tidak ada hubungan yang signifikan antara preferred podcast duration dan listening frequency pada tingkat signifikansi **0.05 (atau 5%)** . Oleh karena itu, saya menjadikan hasil analisis ini sebagai acuan dalam memutuskan atribut yang akan digunakan pada rekomendasi podcast.


# **D. Data Preparation**

Dalam tahap ini, saya menggunakan dua pendekatan untuk membangun sistem rekomendasi berbasis kemiripan: TF-IDF + Cosine Similarity dan Label Encoding + Jaccard Similarity. Keduanya memiliki pendekatan pemrosesan yang berbeda.

**Data Preparation Rekomendasi Musik**

1. TF-IDF + Cosine Similarity
  Tujuan: Mengubah fitur kategorikal menjadi representasi teks untuk dihitung kemiripannya menggunakan TF-IDF dan Cosine Similarity.
  Langkah:
  - Menggabungkan semua nilai fitur menjadi satu string per baris (music_feature_text).
  - TF-IDF akan memberikan bobot pentingnya tiap kata (fitur) berdasarkan frekuensinya.

2.  Label Encoding + Jaccard Similarity
  Tujuan: Mengubah data kategorikal menjadi format numerik menggunakan LabelEncoder agar dapat dihitung kemiripannya dengan Jaccard Similarity.
  Langkah:
  - Setiap nilai unik diubah menjadi angka.
  - Hasil encoding digabung dalam music_feature_vector.

🔄 Perbandingan Singkat
Aspek	TF-IDF + Cosine Similarity	Label Encoding + Jaccard
Representasi Data	Teks (berbobot)	Numerik diskrit
Teknik Kemiripan	Cosine Similarity	Jaccard Similarity
Kelebihan	Menangkap bobot penting fitur	Ringan & cocok untuk biner
Kekurangan	Lebih kompleks	Tidak mempertimbangkan bobot

# E. Modelling


**Membentuk Feature Vector**
Menggabungkan semua nilai fitur kategorikal menjadi satu string per baris.
Digunakan sebagai representasi profil item (lagu/podcast) yang akan dibandingkan antar item.

**Jaccard Similarity**
menghitung seberapa mirip dua item berdasarkan fitur kategorikal.
Output: matriks kemiripan antar item (lagu ke lagu / podcast ke podcast).

**Fungsi Rekomendasi top-N**

# F. EVALUASI 






















