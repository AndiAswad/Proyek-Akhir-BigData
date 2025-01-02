# Nama Anggota Kelompok
   ## Andi Aswad (202110370311029)
   ## Umi Nursyafika (202110370311334)
   ## Gusnaba Fata Kusuma (202110370311037)



# Mencari Jejak Emosi Musik: Analisis Sentimen Musik

## 1. Pendahuluan

### Pernyataan Masalah
Musik memiliki dampak emosional besar pada kehidupan manusia. Namun, bagaimana atribut musik memengaruhi suasana hati (emosi) belum sepenuhnya dipahami. Penelitian ini bertujuan untuk menjawab pertanyaan:
- Apakah emosi dalam musik dapat didefinisikan berdasarkan fitur audio seperti valence, energy, atau danceability?
- Bagaimana genre atau tahun rilis memengaruhi emosi musik?

#### Mengapa ini Menarik?
Hasilnya bermanfaat untuk berbagai pihak, mulai dari platform streaming yang ingin menyempurnakan personalisasi hingga terapi musik yang memanfaatkan hubungan musik dan emosi.

### Rencana dan Metodologi
Data yang digunakan adalah dataset Spotify yang mencakup atribut musik seperti valence, energy, dan danceability. Pendekatan meliputi:
- Pembersihan data.
- Analisis deskriptif dan eksplorasi fitur-fitur utama.
- Visualisasi pola emosi berdasarkan genre dan tren waktu.
- Pengelompokan data untuk menemukan subkelompok penting.

### Teknik Analisis yang Diusulkan
Pendekatan melibatkan:
- Statistik deskriptif untuk memahami distribusi emosi.
- Korelasi untuk mengeksplorasi hubungan antar variabel.
- Clustering untuk mengidentifikasi kelompok musik berdasarkan emosi.

### Manfaat Analisis
Wawasan ini dapat digunakan untuk:
- Membuat playlist yang disesuaikan dengan emosi.
- Mengidentifikasi tren emosi musik dari waktu ke waktu.
- Memberikan panduan untuk terapi musik berbasis suasana hati.

---

## 2. Package yang Diperlukan
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans
```

---

## 3. Data Preparation

### Deskripsi Data
Beberapa variabel penting untuk analisis ini:
- **Valence**: Tingkat emosi positif sebuah lagu.
- **Energy**: Intensitas dan aktivitas sebuah lagu.
- **Danceability**: Kesesuaian lagu untuk menari.

### Langkah Pembersihan Data
- Periksa nilai hilang dan lakukan imputasi jika diperlukan.
- Konversi tipe data seperti `track_album_release_date` menjadi tipe waktu.
- Filter hanya kolom yang relevan untuk analisis.

### Tampilan Data Akhir
```python
spotify_cleaned = spotify[['playlist_genre', 'valence', 'energy', 'danceability', 'track_album_release_date']]
spotify_cleaned.head()
```

### Ringkasan Variabel
Gunakan deskripsi statistik:
```python
spotify_cleaned.describe()
```

---

## 4. Eksplorasi dan Analisis Data

### Informasi Baru dari Data
- Buat variabel baru seperti "Tahun Rilis" dari `track_album_release_date`.
- Hitung rata-rata valence per genre untuk melihat distribusi emosi.

### Temuan dalam Bentuk Visual
#### Distribusi Valence Berdasarkan Genre
```python
sns.boxplot(data=spotify_cleaned, x='playlist_genre', y='valence')
plt.title('Distribusi Valence Berdasarkan Genre')
plt.show()
```

### Hasil Analisis Grafik

1. **Distribusi Valence dan Energy**
   - Lagu dengan energy tinggi lebih umum dibandingkan lagu dengan valence tinggi.
   - Valence memiliki distribusi lebih merata, menunjukkan beragam emosi dalam musik.

2. **Tren Rata-rata Valence dan Energy Berdasarkan Tahun**
   - Energy cenderung meningkat dari tahun ke tahun, mencerminkan tren musik yang lebih dinamis.
   - Penurunan valence menunjukkan pergeseran emosi dalam musik modern menuju tema yang lebih kompleks atau gelap.

3. **Clustering Lagu Berdasarkan Valence dan Energy**
   - Pengelompokan menunjukkan adanya tiga kelompok lagu dengan karakteristik emosi dan intensitas yang berbeda.

4. **Distribusi Valence Berdasarkan Genre**
   - Genre seperti "latin" dan "pop" menunjukkan valence lebih tinggi, sementara "rap" dan "edm" cenderung memiliki valence lebih rendah.


### Tabel Ringkasan
Rata-rata valence dan energy per genre:
```python
summary = spotify_cleaned.groupby('playlist_genre')[['valence', 'energy']].mean().reset_index()
summary
```

| Playlist Genre | Valence  | Energy   |
|----------------|----------|----------|
| EDM            | 0.400656 | 0.802476 |
| Latin          | 0.605510 | 0.708312 |
| Pop            | 0.503521 | 0.701028 |
| R&B            | 0.531231 | 0.590934 |
| Rap            | 0.505090 | 0.650708 |
| Rock           | 0.537352 | 0.732813 |

---

## 5. Rangkuman

### Pernyataan Masalah
Bagaimana atribut musik memengaruhi emosi?

### Metodologi
Dataset Spotify dianalisis dengan statistik deskriptif, visualisasi, dan clustering.

### Wawasan Menarik
- Genre memengaruhi emosi yang dirasakan.
- Tren waktu menunjukkan musik menjadi lebih intens tetapi kurang positif.

### Implikasi untuk Konsumen
Platform streaming dapat meningkatkan pengalaman pengguna dengan rekomendasi berbasis emosi.

### Keterbatasan dan Peningkatan
- **Keterbatasan**: Tidak ada data eksplisit tentang emosi pendengar.
- **Peningkatan**: Integrasi data survei tentang suasana hati pendengar.

### Kesimpulan Hasil Grafik
- Musik modern menunjukkan tren peningkatan intensitas (energy) namun penurunan emosi positif (valence).
- Genre memiliki pengaruh yang signifikan terhadap distribusi emosi dalam lagu.
- Clustering menunjukkan pola yang berguna untuk memahami karakteristik emosional musik.
