
# Songs Recommendadtion

## Project Overview
  
Dalam era digital saat ini, layanan streaming musik seperti Spotify telah menjadi salah satu platform utama bagi pengguna untuk mendengarkan musik secara online. Namun, dengan begitu banyaknya pilihan lagu yang tersedia, seringkali pengguna merasa kesulitan untuk menemukan lagu-lagu yang sesuai dengan preferensi mereka. Inilah mengapa sistem rekomendasi lagu menjadi sangat penting.

Proyek ini bertujuan untuk mengatasi masalah tersebut dengan membangun sistem rekomendasi lagu berdasarkan dataset Spotify. Dengan menggunakan data yang ada, sistem ini akan menganalisis preferensi mendengarkan musik pengguna dan memberikan rekomendasi lagu-lagu yang sesuai.

Salah satu permasalahan yang dihadapi oleh pengguna adalah kesulitan dalam menemukan lagu baru yang sesuai dengan selera mereka. Dengan adanya sistem rekomendasi yang baik, pengguna dapat menemukan lagu-lagu baru yang mungkin tidak akan mereka temukan secara manual, meningkatkan kepuasan mereka dalam menggunakan layanan streaming musik.

Contoh konkret dari permasalahan ini adalah ketika pengguna ingin menjelajahi genre musik baru atau menemukan lagu-lagu serupa dengan yang sedang mereka dengarkan. Dengan sistem rekomendasi yang efektif, pengguna dapat dengan mudah menemukan lagu-lagu yang sesuai dengan preferensi mereka tanpa harus melakukan pencarian manual yang rumit.

Hasil dari proyek ini diharapkan dapat diterapkan secara langsung kepada pengguna aplikasi streaming musik, membantu mereka menemukan lagu-lagu baru yang mereka sukai dan meningkatkan pengalaman mendengarkan musik mereka secara keseluruhan.


## Business Understanding

### Problem Statements
1.  Pengguna kesulitan menemukan lagu baru yang sesuai dengan selera mereka.
2.  Pengguna ingin menjelajahi genre musik baru, tetapi tidak tahu harus mulai dari mana dan ingin rekomendasi yang dipersonalisasi.

### Goals
1.  Mengembangkan sistem rekomendasi lagu yang dapat memberikan rekomendasi yang relevan dan personal kepada pengguna.
2.  Meningkatkan retensi pengguna dan kepuasan pelanggan dengan meningkatkan kualitas rekomendasi lagu dengan rekomendasi yang membantu pengguna dalam eksplorasi genre musik baru serta dipersonalisasi.

### Solution Approach
####  Solution statements
1.  Mengimplementasikan *content-based filtering* untuk memperkuat rekomendasi dengan mempertimbangkan fitur lagu seperti tempo dan valence.
2.  Meningkatkan kualitas rekomendasi dengan memanfaatkan algoritma yang dapat mempelajari pola preferensi pengguna dari interaksi sebelumnya sehingga memberikan rekomendasi yang lebih sesuai.

Dengan mengadopsi pendekatan *content-based filtering*, sistem rekomendasi akan dapat memberikan rekomendasi yang lebih relevan dengan menganalisis fitur-fitur intrinsik dari lagu-lagu yang telah didengarkan oleh pengguna. Selain itu, dengan memanfaatkan algoritma yang dapat mempelajari pola preferensi pengguna, sistem ini akan dapat memberikan rekomendasi yang semakin dipersonalisasi seiring waktu, meningkatkan retensi pengguna dan kepuasan pelanggan.

Stakeholder utama dari proyek ini adalah pengguna layanan streaming musik, yang akan mendapatkan manfaat langsung dari rekomendasi lagu yang lebih relevan dan personal. Selain itu, platform streaming musik juga akan mendapatkan manfaat dengan meningkatnya retensi pengguna dan kepuasan pelanggan, yang pada waktunya akan dapat meningkatkan loyalitas pengguna dan pendapatan platform. Dengan memperbaiki kualitas rekomendasi lagu, proyek ini diharapkan dapat memberikan dampak positif bagi bisnis dan ekonomi secara keseluruhan.

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

Dalam memilih algoritma/model untuk menyelesaikan permasalahan yang diangkat pada proyek ini akan menggunakan *cosine similarity* dan *content-based filtering*. Alasan utama penggunaan *cosine similarity* adalah karena metode ini cocok untuk sistem rekomendasi berbasis konten, di mana kita ingin menemukan kesamaan antara item berdasarkan fitur-fitur atau karakteristik intrinsiknya. Dalam konteks ini, kita ingin merekomendasikan lagu-lagu yang mirip berdasarkan fitur-fitur seperti tempo, valence, dan genre.

Selain itu, *cosine similarity* juga memiliki keunggulan dalam menangani data berdimensi tinggi dan tidak rentan terhadap perubahan skala, sehingga cocok untuk data musik yang biasanya memiliki banyak fitur numerik.

Penggunaan *content-based filtering* juga memberikan keleluasaan dalam membuat rekomendasi yang lebih dipersonalisasi untuk pengguna, tanpa memerlukan data historis interaksi dari pengguna. Hal ini menjadikan *content-based filtering* sebagai pilihan yang sesuai untuk proyek ini, di mana kita ingin memberikan rekomendasi yang relevan berdasarkan fitur-fitur intrinsik lagu.

Dengan demikian, penggunaan *cosine similarity* dan *content-based filtering* dipilih karena kecocokannya dengan karakteristik data dan kebutuhan proyek, serta kemampuannya untuk memberikan rekomendasi yang lebih relevan dan dipersonalisasi kepada pengguna.

Dalam membangun rekomendasi sistem nya, melakukan `cosine_similarity()`  terhadap data numerical, setelah itu menambahkan satu kolom baru sebagai penanda index baris unik pada setiap baris data menggunakan `LabelEncoder()`. 

Rumus untuk cosine similarity antara dua vektor **A** dan **B** dapat ditulis sebagai berikut:

$$cos(\theta) =  \frac{A . B} {||A|| .||B||} = \frac{
\sum_{i=1}^n A_i B_i }{  \sum_{i=1}^n A_i^2   \sum_{i=1}^n B_i^2 }
$$

Di sini:
-   A dan B adalah dua vektor yang ingin dibandingkan.
-   ⋅ adalah operator dot product (produk dot) antara vektor A dan B.

Setelah itu membuat satu function untuk memanggil rekomendasi lagunya, dengan beberapa pengkondisian seperti apakah hanya merekomendasikan genre lagu yang sama atau tidak dan juga menentukan jumlah rekomendasi yang diberikan.

Berikut hasil dari rekomendasi terhadap lagu 'City Of Lights - Official Radio Edit' : 

|index|Artist|Song|Genre|
|---|---|---|---|
|0|Bro Safari|Drama \(Party Favor Remix\)|edm|
|1|Incubite|Glowstix, Neon & Blood|pop|
|2|Lucky Luke|E\.B\.Y\.T\.|edm|
|3|Javiera Mena|Acá Entera|pop|
|4|Getfar|Shining Star \(Vocal Mix\)|edm|

## Evaluation
### Formula Metrik Evaluasi: Precision

Precision dalam konteks content-based filtering dapat dihitung dengan rumus berikut:

$$Precision=\frac{Jumlah rekomendasi yang relevan} {Jumlah total rekomendasi}​$$

Dalam konteks sistem rekomendasi lagu berbasis konten, rekomendasi yang relevan adalah lagu-lagu yang memiliki kemiripan tinggi dengan lagu yang sedang didengarkan atau dipilih oleh pengguna. Jumlah total rekomendasi adalah jumlah lagu yang direkomendasikan oleh sistem.

### Hasil Metrik Evaluasi

Dengan menggunakan metrik precision, dapat mengevaluasi seberapa baik sistem rekomendasi lagu berbasis konten dalam memberikan rekomendasi yang relevan kepada pengguna. Hasil evaluasi metrik precision yang tinggi menunjukkan bahwa sistem rekomendasi mampu memberikan rekomendasi lagu yang sesuai dengan preferensi pengguna.

Dalam konteks proyek ini, hasil dari metric precision diperoleh dari 2 pengujian, yang pertama menggunakan perbandingan total jumlah nilai dari kolom *'danceability',  'energy',  'loudness',  'mode',  'speechiness', 'acousticness',  'instrumentalness',  'liveness',  'valence',  'tempo'*  pada data inputan pengguna dengan total jumlah nilai dari kolom yang sama pada setiap hasil rekomendasi sistem. 

Nilai total dari kolom-kolom tersebut pada lagu *'City Of Lights - Official Radio Edit'* adalah 129.153 dan nilai pada hasil rekomendasi secara berurut adalah 99.964975,  126.817183, 123.111700, 117.229400 dan 124.741140. Dengan menetapkan suatu threshold sebagai pertimbangan selisih sebesar 15, maka  4 dari 5 rekomendasi yang diberikan cukup sesuai dengan data (80% rekomendasi). 

Pengujian lainnya menggunakan kecocokan genre lagu yang dihasilkan oleh rekomendasi sistem dengan genre lagu inputan pengguna. Pada kasus ini lagu *City Of Lights - Official Radio Edit* ber-genre edm dan hasil rekomendasi 3 dari 5 menampilkan lagu dengan genre edm.

Secara keseluruhan model dapat menyelesaikan dan memberikan solusi terhadap permasalahan pengguna dengan memberikan rekomendasi lagu berdasarkan lagu yang sedang didengar oleh pengguna dan personalisasi serta lebih relevan untuk diputar selanjutnya sehingga memenuhi *goals* atau tujuan dari proyek ini.
