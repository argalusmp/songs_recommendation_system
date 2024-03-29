
# Laporan Proyek Machine Learning - Vidi Septri Argalus Mp

## Project Overview

Dalam proyek ini,  bertujuan untuk membangun sistem rekomendasi lagu berdasarkan dataset Spotify. Sistem rekomendasi ini akan membantu pengguna menemukan lagu-lagu yang sesuai dengan preferensi mereka, berdasarkan lagu yang telah mereka dengarkan sebelumnya. Sistem rekomendasi dapat membantu meningkatkan pengalaman mendengarkan musik pengguna.

Sistem rekomendasi memiliki dampak yang signifikan terhadap kepuasan user ketika berinteraksi dengan aplikasi, antara lain:
-   Meningkatkan pengalaman mendengarkan musik pengguna.
-   Membantu pengguna menemukan musik baru yang mereka sukai.
-   Memberikan solusi bagi pengguna yang ingin menjelajahi genre musik baru.

## Business Understanding

### Problem Statements
1.  Pengguna kesulitan menemukan lagu baru yang sesuai dengan selera mereka.
2.  Pengguna ingin menjelajahi genre musik baru, tetapi tidak tahu harus mulai dari mana.
3.  Pengguna ingin mendapatkan rekomendasi lagu yang dipersonalisasi.

### Goals
1.  Mengembangkan sistem rekomendasi lagu yang dapat memberikan rekomendasi yang relevan dan personal kepada pengguna.
2.  Meningkatkan retensi pengguna dan kepuasan pelanggan dengan meningkatkan kualitas rekomendasi lagu.

### Solution Approach
####  Solution statements
Mengimplementasikan *content-based filtering* untuk memperkuat rekomendasi dengan mempertimbangkan fitur lagu seperti  tempo dan *valence*.

## Data Understanding
Data yang digunakan adalah dataset Spotify yang berisi informasi tentang lagu-lagu, termasuk nama lagu, artis, genre, dan fitur audio seperti *danceability*, *energy*, dan *valence*. Dataset ini diambil dari Kaggle: [Spotify Dataset](https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs/data).
Dataset ini terdiri dari sejumlah kolom data, antara lain:
- track_id : sebagai *ID* unik dari lagu
- track_name : nama lagu
- track_artist : nama penyayi
- track_popularity : kepopularitasan dari lagu (0-100), dimana lebih tinggi lebih bagus
- track_album_id : sebagai *ID* unik dari album
- track_album_name : nama dari album
- track_album_release_date : tanggal ketika album rilis
- playlist_name : nama *playlist*
- playlist_id : sebagai ID unik dari *playlist*
- playlist_genre : nama genre dari *playlist*
- playlist_subgenre : nama subgenre dari playlist
- danceability : menunjukkan seberapa cocok musik untuk menari berdasarkan kombinasi elemen musik
- energy : estimasi 0.0 sampai 1.0 dan merepresentasikan rasa musik seperti tempo cepat, keras ataupun berisik
- key : notasi kunci yang digunakan
- loudness : kekuatan dari suara dalam *decibels* (dB)
- mode : indikasi major atau minor dari lagu
- speechiness : mendeteksi bagaimana lirik lagu dinyanyikan
- acousticness : mengukur seberapa akustik lagu tersebut
- instrumentalness : mengukur seberapa instrumental lagu berdasarkan ada tidak vokal penyanyi
- liveness : akurasi ada tidak nya penonton ketika rekaman 0.0 - 1.0
- valence : mendeskripsikan nuansa yang positif seperti senang dan bahagia dari lagu
- tempo : pengukuran tempo berdasarkan *beats per minute* (BPM)
- duration_ms : durasi lagu dalam milidetik

### Exploratory Data Analys

Gambar 1. Playlist terpopuler berdasarkan genre
![GitHub Image](https://github.com/argalusmp/songs_recommendation_system/blob/main/images/Screenshot%202024-03-29%20143119.png?raw=true)
Pada Gambar 1, dapat dilihat bahwa lagu yang paling populer berada pada sub genre *post-teen po, hip hop, permanent wave* dan *dance pop*.

Gambar 2. Lagu yang *danceability*
![GitHub Image](https://github.com/argalusmp/songs_recommendation_system/blob/main/images/Screenshot%202024-03-29%20143323.png?raw=true)
Gambar 2, menunjukkan bahwa genre *latin* dan *rap* paling mendominasi dalam komposisi musik yang cocok sambil menari.

Gambar 3.  Penanyi dengan akumulasi popularitas tinggi
![Github Image](https://github.com/argalusmp/songs_recommendation_system/blob/main/images/Screenshot%202024-03-29%20143351.png?raw=true)
Pada Gambar 3, menunjukkan akumulasi popularitas penyanyi-penyayi berdasarkan yang didapat dari lagu yang mereka miliki.

Gambar 4. Genre musik yang paling *energy*
![Github Image](https://github.com/argalusmp/songs_recommendation_system/blob/main/images/Screenshot%202024-03-29%20143405.png?raw=true)
Gambar 4 ini menunjukkan bahwa genre edm, rock, pop, dan latin paling mendominasi jenis musik yang memiliki iinstrumen paling energik pada lagunya.

Tabel 1. Lagu yang paling menyebarkan nilai positive
|index|track\_artist|track\_album\_name|playlist\_name|playlist\_genre|valence|
|---|---|---|---|---|---|
|13531|War|The Very Best Of War|70's Classic Rock|rock|0\.991|
|22762|War|Why Can't We Be Friends?|The 1950s/1960s/1970s/1980s/1990s/2000s/2010s with pop/r&b/soul/boogie/dance/jazz/hip hop/hop/rap\.|r&b|0\.99|
|12710|The Doobie Brothers|Minute By Minute|Soft Rock Drive|rock|0\.985|
|26302|1986 Omega Tribe|Crystal Night|Japanese Funk/Soul/NEO/Jazz/Acid|r&b|0\.984|
|31680|Soulsearcher|Can't Get Enough|House/Electro/Progressive/Disco/Lofi/Synthwave|edm|0\.983|

Berdasarkan Tabel 1, lagu *rock, r&b* memiliki suasana lagu yang dapat menyebarkan vibes positive terhadap pendengarnya.

## Data Preparation
Tahapan data preparation yang dilakukan meliputi:
-   Pengecekan dan mengatasi *null value*
Pada bagian ini mengecek apakah data memiliki *null value* dan memutuskan untuk *drop rows*, karena jumlah *null value* sangat sedikit sehingga tida berpengaruh pada keseluruhan data.

|index|Counts|Uniqueness|null|Datatype|
|---|---|---|---|---|
|track\_id|32833|28356|0|object|
|track\_name|32833|23449|5|object|
|track\_artist|32833|10692|5|object|
|track\_popularity|32833|101|0|int64|
|track\_album\_id|32833|22545|0|object|
|track\_album\_name|32833|19743|5|object|
|track\_album\_release\_date|32833|4530|0|object|
|playlist\_name|32833|449|0|object|
|playlist\_id|32833|471|0|object|
|playlist\_genre|32833|6|0|object|
|playlist\_subgenre|32833|24|0|object|
|danceability|32833|822|0|float64|
|energy|32833|952|0|float64|
|key|32833|12|0|int64|
|loudness|32833|10222|0|float64|
|mode|32833|2|0|int64|
|speechiness|32833|1270|0|float64|
|acousticness|32833|3731|0|float64|
|instrumentalness|32833|4729|0|float64|
|liveness|32833|1624|0|float64|
|valence|32833|1362|0|float64|
|tempo|32833|17684|0|float64|
|duration\_ms|32833|19785|0|int64|

-   Penghapusan kolom data yang tidak dibutuhkan
Beberapa kolom data untuk pengembangan model ini tidak dibutuhkan sehingga lebih baik untuk men-*drop* dari dataframe, antara lain *'track_id', ' playlist_id', 'track_album_id', 'duration_ms'* dan *'track_album_release_date'*

-   Melakukan *split* pada *categorical* dan *numerical* kolom data agar kolom numerical dapat digunakan untuk model.

## Modeling
Dalam membangun rekomendasi sistem nya, melakukan `cosine_similarity()`  terhadap data numerical, setelah itu menambahkan satu kolom baru sebagai penanda index baris unik pada setiap baris data menggunakan `LabelEncoder()`. 

Setelah itu membuat satu function untuk memanggil rekomendasi lagunya, dengan beberapa pengkondisian seperti apakah hanya merekomendasikan genre lagu yang sama atau tidak dan juga menentukan jumlah rekomendasi yang diberikan.

Berikut hasil dari rekomendasi terhadap lagu 'Someone You Loved - Future Humans Remix' : 

|index|Artist|Song|Genre|
|---|---|---|---|
|0|Hardwell|Baldadig|latin|
|1|La Fouine|Terminus|r&b|
|2|Green Tea|People Be Watchin|r&b|
|3|ICEHOUSE|Great Southern Land - Remastered|pop|
|4|Sammy Milo|Eine Keine Meine|edm|
|5|Ram Jam|Black betty|rock|
|6|Depeche Mode|Get The Balance Right\! - Combination Mix|pop|
|7|Kurdo|Mike Tyson - Bonustrack|rap|
|8|Jessica Reedy|God Has Smiled On Me|r&b|
|9|Rick Ross|The Devil Is A Lie|rap|

## Evaluation
Metric yang digunakan untuk membangun model ini adalah cosine similarity dimana menemukan kemiripan antar nilai vector pada data, disini model dibangun atas cosine similarity terhadap data-data numerical seperti '*track_popularity', 'danceability', 'energy', 'key', 'loudness',  'mode', 'speechiness', 'acousticness', 'instrumentalness', 'liveness',  'valence', 'tempo'*. Sehingga ini akan menghasilkan rekomendasi lagu-lagu yang memiliki kedekatan atau kemiripan dengan nilai-nilai vector lagu yang di-input atau sedang didengarkan oleh pengguna.

Rumus untuk cosine similarity antara dua vektor **A** dan **B** dapat ditulis sebagai berikut:
![](https://miro.medium.com/v2/resize:fit:1400/1*LfW66-WsYkFqWc4XYJbEJg.png)
Di sini:
-   A dan B adalah dua vektor yang ingin dibandingkan.
-   ⋅ adalah operator dot product (produk dot) antara vektor A dan B.

Secara keseluruhan model dapat menyelesaikan dan memberikan solusi terhadap permasalahan pengguna dengan memberikan rekomendasi lagu berdasarkan lagu yang sedang didengar oleh pengguna dengan lebih relevan untuk diputar selanjutnya.
