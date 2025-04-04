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

#**B. Business Understanding**

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
##EDA - Deskripsi Variabel
