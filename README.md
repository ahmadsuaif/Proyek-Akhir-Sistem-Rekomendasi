# Laporan Proyek Machine Learning - Sistem Rekomendasi Aplikasi

## Project Overview

Google Play adalah toko online yang sangat popluer untuk menemukan aplikasi, game, film, acara TV, buku, dan konten lainnya. Google Play menyediakan 2 juta aplikasi & game untuk miliaran orang di seluruh dunia. Google Play adalah toko online yang dikunjungi pengguna untuk menemukan aplikasi, game, film, acara TV, buku, dan konten lainnya.  Setiap harinya Google Play dibanjiri oleh banyak aplikasi baru yang dibuat oleh para pengembang aplikasi. Hal ini tentunya berdampak positif bagi pengguna karena dihadapkan lebih banyak pilihan aplikasi yang bisa di-install. Namun hal ini tentunya juga akan membuat pengguna bingung memilih aplikasi yang paling sesuai dengan kebutuhannya [[1](https://irjet.com/archives/V8/i4/IRJET-V8I4745.pdf)]. 

Sistem rekomendasi merupakan sistem yang memberikan rekomendasi pada suatu item yang dapat digunakan untuk membantu user dalam mengambil keputusan. [[2](https://www.researchgate.net/publication/220604600_Recommender_Systems_An_Overview)] [[3](https://www.researchgate.net/publication/258651634_A_Study_of_Recommender_System_Techniques)] [[4](https://www.researchgate.net/publication/281705736_Decision-making_in_recommender_systems_The_role_of_user's_goals_and_bounded_resources)]. Dalam hal pengambilan keputusan guna memilih aplikasi yang paling sesuai untuk di-install pengguna Google Play, maka tentunya pengembangan sistem rekomendasi merupakan hal yang akan sangat membantu pengguna.

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan [[5](https://www.researchgate.net/publication/331063850_Recommender_Systems_Challenges_and_Solutions_Survey)], Pada sistem rekomendasi aplikasi faktor-faktor yang bisa menjadi bahan pertimbangan antara lain seperti Category,	Rating,	Reviews, Size, Installs,	Type,	Price,	Content, Rating,	Genres,	Last Updated,	Current Ver,	Android Ver, dan faktor-faktor lainnya. Karena model sistem rekomendasi yang akan dikembangkan pada proyek ini yaitu model Content Based Filtering dan Collaborative Filtering, sehingga faktor-faktor yang akan dipelajari pada proyek ini adalah Category dan Rating. Untuk faktor-faktor lainnya seperti Reviews, Size, Installs,	Type,	Price,	Content, Rating,	Genres,	Last Updated,	Current Ver,	Android Ver, dan faktor-faktor lainnya akan dipelajari pada pengembangan model lebih lanjut nantinya.

## Business Understanding

Pengembangan model Sistem Rekomendasi Aplikasi tentunya memiliki potensi dampak atau manfaat berupa menjadi salah satu alat bantu dalam pengambilan keputusan oleh pengguna Google Play.
Contoh potensi manfaat dari Sistem Rekomendasi Aplikasi ini adalah membantu pengguna Google Play membuat keputusan instalasi suatu aplikasi dengan lebih bijaksana.

### Problem Statements
- Berdasarkan eksplorasi *dataset*, bagaimana karakteristik dataset? Ada berapa banyak jumlah data? Fitur apa yang bisa dipilih untuk pengembangan model?
- Pada bagian Data Assesing, apakah terdapat terdapat data duplikat dan data missing? Jika ada tindakan apa yang paling tepat untuk diterapkan?
- Pada bagian Data Cleaning, apakah perlu dilakukan tindakan dropping ataupun imputation untuk memamstikan data layal digunakan untuk pengembangan model?
- Bagaimana mengolah *dataset* agar dapat dibuat model sistem rekomendasi?
- Bagimana membuat model sistem rekomendasi Content Based Filtering dan Collaborative Filtering?
- Bagaimanna cara mengukur nilai perfoma model sistem rekomendasi yang telah dibangun?

### Goals
- Mengeksplorasi informasi *dataset* dan melihat fitur yang paling memungkinkan dipilih untuk pengembangan model
- Melakukan proses Data Assesing untuk melihat kemungkinan adanya data duplikat dan data missing
- Melakukan proses Data Cleaning dan melakukan tindakan yang paling tepat untuk membersihkan data untuk kemudian siap digunakan untuk pengembangan model
- Melakukan proses Data Preparation seperti Vectorizing dan Data Spliting sebelum pembuatan model
- Membuat model sistem rekomendasi Content Based Filtering dan Collaborative Filtering berdasarkan fitur yang telah dipilih dari dataset
- Mengukur perfoma model sistem rekomendasi dengan menggunakan metrik evaluasi


### Solution Approach
- Untuk eksplorasi fitur dilakukan Analisis Univariat. Analisis Univariat dilakukan untuk mengeksplorasi distribusi suatu fitur yang dipilih dalam suatu dataset. Teknik yang digunakan adalah menggunakan visualiasi data menggunakan barplot dari fitur yang dipilih.
- Agar didapatkan model prediksi yang baik maka dilakukan proses *Data Wragling* yang meliputi *Data Gathering*, *Data Assessing*, dan *Data Cleaning*.
- Untuk mengetahui perfoma model dilakukan pengecekan performa dengan metrik evaluasi seperti Precission, MAE dan RMSE.

## Data Understanding
Data yang digunakan dalam pembuatan model merupakan data sekunder. Data diambil dari Kaggle dengan nama *dataset* yaitu *California House Price*. 

URL: [https://www.kaggle.com/*dataset*s/shibumohapatra/house-price](https://www.kaggle.com/datasets/lava18/google-play-store-apps)

Berikut merupakan detail dari *dataset* yang digunakan untuk pembuatan model:
- Dataset berupa 3 buah file CSV yaitu googleplaystore.csv, googleplaystore_user_reviews.csv, dan license.txt
- Dataset yang digunakan dalam proyek ini yaitu googleplaystore.csv
- Dataset terdiri dari 10841 entri dengan 13 fitur.
- Dataset terdiri dari 12 data kategori dan 1 data numerik.
- Dataset memiliki *missing value* sejumlah 1474 pada Rating, 1 pada Type, 1 pada Content Rating, 8 pada Current Ver, dan 3 pada Android Ver.
  
### Variabel-variabel pada *dataset* adalah sebagai berikut:
- App                  : nama aplikasi
- Category             : kategori aplikasi
- Rating               : penilaian pengguna dari aplikasi (dalam satuan bintang 1-5)
- Reviews              : jumlah pengguna yang memberikan ulasan pada aplikasi tersebut (dalam satuan buah)
- Size                 : ukuran dari aplikasi (dalam satuan byte)
- Installs             : jumlah pengguna yang meng-install aplikasi
- Type                 : tipe aplikasi (dalam kategori Paid/berbayar atau Free/gratis)
- Price                : harga dari aplikasi (dalam satuan dollar USD)
- Content Rating       : kategori usia penggunaan untuk aplikasi (Everyone, Mature 17+, dst)
- Genres               : kategori dari genre aplikasi (Medical, Lifestyle, dst)
- Last Updated         : tanggal terakhir aplikasi di perbaharui oleh pengembang aplikasi
- Current Ver          : versi terkini dari aplikasi
- Android Ver          : versi android minimum yang dipersyaratkan untuk meng-install aplikasi

Untuk memahami data lebih lanjut, dilakukan Analisis Univariat serta Visualisasi Data

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel.  Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu *dataset*. Sebagai alat bantu analisis, dilakukan teknik Visualisasi Data. Memvisualisasikan data memberikan wawasan mendalam tentang perilaku berbagai fitur-fitur yang tersedia dalam *dataset*. Teknik visualisasi yang digunakan pada pembuatan model proyek ini adalah dengan menggunakan barplot yang digunakan untuk memplot distribusi data.

Berikut adalah hasil Exploratory Data Analysis (EDA) menggunkan Analisis Univariat dengan teknik Visualisasi Data  menggunakan barplot.
![download (2)](https://github.com/ahmadsuaif/Proyek-Pertama-Predictive-Analytics/assets/66425290/97c7ccca-2ef8-4f02-aefa-e847c902dc25)

Gambar 1a. Analisis Univariat (Data Kategori)

![download (3)](https://github.com/ahmadsuaif/Proyek-Pertama-Predictive-Analytics/assets/66425290/5e4ae928-6257-4694-a78f-b538141ffc9c)

Gambar 1b. Analisis Univariat (Data Numerik)

Berdasarkan Gambar 1a , dapat dilihat bahwa distribusi data kategori untuk 'ocean_proximity' memiliki perbandingan jumlah yang tidak sama, untuk nilai data '<1H OCEAN' berjumlah 7607 dengan persentase 43.2% sedangkan nilai data 'ISLAND' hanya berjumlah 5. Lebih jauh, pada Gambar 1b, untuk data numerik memiliki karakteristik, yaitu:
- koordinat longitude rumah mayoritas berada pada -118 derajat dan -122 derajat dan koordinat latitude rumah mayoritas berada pada 34 derajat dan 38 derajat
- median dari umur rumah banyak terdistribusi pada rentang umur 10 - 40, namun nilai terbanyak terdapat pada nilai 50.
- rata-rata terbanyak untuk data total room dan total bedroom yaitu di antara angka 1000-2000 room dan 200-400 bedroom.
- rata-rata terbanyak untuk data population dan households berada di antara angka 500-1000 dan 200-400.
- median income dan median house value terbanyak masing-masing berada di antara angka 3 dan 200000.
- distribusi median house value miring ke kanan (right-skewed). Hal ini akan berimplikasi pada model.
  
## Data Preparation
Pada proses *Data Preparation* dilakukan kegiatan seperti *Data Gathering*, *Data Assessing*, dan *Data Cleaning*.
Pada proses *Data Gathering*, data diimpor sedemikian rupa agar bisa dibaca dengan baik menggunakan *datafram*e Pandas.
Untuk proses *Data Assessing*, berikut adalah beberapa pengecekan yang dilakukan:
- Duplicate data (data yang serupa dengan data lainnya)
- Missing value (data atau informasi yang "hilang" atau tidak tersedia)
- Outlier (data yang menyimpang dari rata-rata sekumpulan data yang ada)
 
Pada proses *Data Cleaning*, secara garis besar, terdapat tiga metode yang dapat digunakan antara lain seperti berikut:
- Dropping (metode yang dilakukan dengan cara menghapus sejumlah baris data)
- Imputation (metode yang dilakukan dengan cara mengganti nilai yang "hilang" atau tidak tersedia dengan nilai tertentu yang bisa berupa median atau mean dari data)
- Interpolation (metode menghasilkan titik-titik data baru dalam suatu jangkauan dari suatu data)

Pada kasus proyek ini tidak ditemukan data duplikat. Pada proyek ini ditemukan *Missing Value*. Adapaun metode yang digunakan untuk mengatasi hal ini adalah dengan menerapkan *imputation* dimana data yang *missing* diganti dengan nilai *mean*. Untuk *outlier* sendiri dilakukan metode *dropping* menggunakan metode IQR. IQR sendiri didapatkan dengan cara mengurangi Q3 dengan Q1 sebagaimana rumusan berikut. 

$$ IQR = Q<sub>3</sub> - Q<sub>1</sub> $$

dimana
Q<sub>1</sub> adalah kuartil pertama dan Q<sub>3</sub> adalah kuartil ketiga.

Dengan menggunakan metode IQR, dapat ditentukan *outlier* melalui suatu nilai batas yang ditentukan. Setelah menggunakan metode IQR dimana *dataset* yang sebelumnya berjumlah 20640 menjadi 17609.
 
Semua proses ini diperlukan dalam rangka membuat model yang baik. 

Untuk mereduksi jumlah fitur dilakukan proses PCA. Teknik reduksi ini adalah prosedur yang mengurangi jumlah fitur dengan tetap mempertahankan informasi pada data. PCA ini adalah teknik untuk mereduksi dimensi, mengekstraksi fitur, dan mentransformasi data dari “n-dimensional space” ke dalam sistem berkoordinat baru dengan dimensi m, di mana m lebih kecil dari n. Pada proyek ini, fitu 'housing_median_age',	'total_rooms',	'total_bedrooms',	'households' divisualisasikan untuk melihat hubungan di antara fitur-fitur tersebut. sperti yang terlihat pada Gambar 3 berikut.

![download (7)](https://github.com/ahmadsuaif/Proyek-Pertama-Predictive-Analytics/assets/66425290/b05e92dd-398d-4932-9ad2-f75400ac1e26)

Gambar 3 Visualisasi Hubungan antar Fitur sebelum Reduksi PCA

Berdasarkan Gambar 3 dapat diketahui yang memiliki hubungan antar fitur hanya tiga yaitu 'total_rooms',	'total_bedrooms',	'households'. Selanjutnya, 3 fitur ini dapat direduksi dengan PCA. Sebelum itu, cek proporsi informasi dari ketiga komponen PCs tadi.

```
pca.explained_variance_ratio_.round(3)
```
Potongan kode tersebut memberikan keluaran berupa array([0.985, 0.014, 0.001]). Berdasarkan hasil ini, yang dipertahankan adalah PC (komponen) pertama saja karena dari output yang dideroleh diketahui bahwa 98.5% informasi pada ketiga fitur 'total_rooms',	'total_bedrooms',	'households' terdapat pada PC pertama. Sedangkan sisanya, sebesar 1.4% dan 0.1% terdapat pada PC kedua dan ketiga. PC pertama ini akan menjadi fitur 'house properties' menggantikan ketiga fitur lainnya ('total_rooms',	'total_bedrooms',	'households').


Setelah data dibersihkan, *dataset* dibagi menjadi data train dan data test untuk proses *Modeling*, dimana rasio pembagian data yang dipilih adalah 90:10 mengingat data test untuk rasio tersebut sudah terbilang cukup. 
Adapun detail dari *dataset* tersebut adalah:
- Total sampel di dalam *dataset* train: 15848
- Total sampel di dalam *dataset* test: 1761

## Modeling
Seperti yang dijelaskan di awal, model yang dipilih adalah model regresi karena merupakan salah satu algoritma yang paling umum digunakan dalam pembuatan model prediksi. Dalam bentuk yang sederhana, regresi terdiri dari intersep dan slope yang dituliskan dalam rumusan berikut

$$ y = a + bX $$

dimana: 
- y adalah variabel kriterium (variabel terikat yang digunakan untuk memprediksi)
- a adalah intersep (variabel konstan yang memiliki arti sebagai titik perpotongan suatu garis dengan sumbu Y),
- b adalah slope (nilai koefisien yang menyatakan ukuran kemiringan suatu garis), dan
- X adalah variabel prediktor (variabel yang digunakan untuk memprediksi atau menjelaskan variabel lain dalam suatu model)

Secara umum, regresi ini itu sendiri digunakan untuk meramalkan pengaruh variabel prediktor terhadap variabel kriterium atau membuktikan ada atau tidaknya hubungan fungsional antara variabel bebas (X) dengan variabel terikat (y).

Namun begitu terdapat kelebihan dan kekurangan dari model regresi, yaitu:

Kelebihan regresi:
- Kemudahan untuk digunakan
- Kekuatan Prediktor dalam mengidentifikasi sekuat apa pengaruh yang diberikan oleh variabel prediktor (variabel independen) terhadap variabel lainnya (variabel dependen).
- Dapat memprediksi nilai/tren di masa yang mendatang

Kelemahan dari model regresi adalah karena hasil ramalan dari analisis regresi merupakan nilai estimasi sehingga kemungkinan untuk tidak sesuai dengan data aktual tetaplah ada.

Pada proyek yang dikerjakan, algoritma regresi yang coba dibandingkan adalah regresi linear, regresi ridge, *random forest regressor*, dan *random forest regressor* dengan hyperparamter tuning. Regresi linear adalah teknik analisis data yang memprediksi nilai data yang tidak diketahui dengan menggunakan nilai data lain yang terkait dan diketahui dimana secara matematis dimodelkan sebagai persamaan linier, regresi ridge merupakan metode estimasi koefisien regresi yang diperoleh melalui penambahan konstanta bias c, dan random forest adalah suatu algoritma yang digunakan pada klasifikasi data dalam jumlah yang besar dimana teknik klasifikasi *random forest* dilakukan melalui penggabungan pohon dengan melakukan training pada sampel data yang dimiliki.

Untuk meningkatkan model, dilakukan *hyperparamter tuning*. Adapun paramater yang di-tuning antara lain n_estimators', 'max_depth', 'min_samples_split', dan 'min_samples_leaf. Untuk memudahkan proses *tuning* digunakan GridSearchCV. GridSearchCV itu sendiri merupakan bagian dari modul scikit-learn yang dapat digunakan untuk mendapatkan nilai *hyperparameter* secara otomatis. Grid Search adalah metode yang digunakan untuk mencari parameter yang paling tepat untuk meningkatkan performa model dengan mencoba seluruh kombinasi *hyperparameter* yang diberikan.

Berikut adalah nilai parameter *tuning*
```
params = {'n_estimators' : [50,80,100],
          'max_depth' : [3,5,10],
           'min_samples_split':[2,3,4],
            'min_samples_leaf': [2,3,4]}
```
Berdasarkan hasil pengujian, terpilih grid.best_params_ yaitu 
```
{'max_depth': 10,
 'min_samples_leaf': 4,
 'min_samples_split': 2,
 'n_estimators': 100}
```
Parameter dengan nilai inilah yang kemudian dibuat sebagai model.

## Evaluation
Adapun metrik yang sebagai alat ukur perfoma model yang dibuat antara lain **MSE · MAE · R<sup>2</sup>**. 

Berikut merupakan rumus dari masing-masing metrik yang digunakan:

$$ MAE = (1/n) Σ |y<sub>i</sub> - ŷ<sub>i</sub>| $$

$$ MSE = (1/n) Σ (y<sub>i</sub> - ŷ<sub>i</sub>)<sup>2</sup> $$

$$ R<sup>2</sup> = 1 - (MSE / Var(y)) $$

y<sub>i</sub> mewakili nilai yang diamati,
ŷ<sub>i</sub> mewakili nilai prediksi,
n adalah jumlah titik data,
Var(y) mewakili varians dari nilai yang diamati.

Berikut merupakan penjelasan kegunaan dari masing-masing metrik yang digunakan:
- MAE menghitung rata-rata dari selisih absolut antara nilai prediksi dan nilai aktual. Semakin kecil nilai MAE, semakin baik kualitas model tersebut.
- MSE menghitung rata-rata dari selisih kuadrat antara nilai prediksi dan nilai aktual. Semakin kecil nilai MSE, semakin baik kualitas model tersebut.
- R<sup>2</sup> digunakan untuk menilai seberapa besar pengaruh variabel independen tertentu terhadap variabel dependen

Tabel 1 berikut merupakan perbandingan 4 buah model yang coba dibandingkan

|     |Model 1|Model 2|Model 3|Model 4|
|---|---|---|---|---|
|R<sup>2</sup>|-7504.309425109431|-7498.0783949337365.146779279|-1.880080745581838|2.432728538383974|
|MSE|8166746.146779279|8163355.360001828|159980.5138016423|174656.3925179131|
|MAE|6509173.648630178|6506404.9997212|133115.5655366269|154364.3230594773|

Tabel 1. Perbandingan Performa MAE, MSE, dan R<sup>2</sup> Model

Berdasarkan Tabel 1, secara umum Model 3 (RF1) dan Model 4 (RF2) menampilkan hasil performa yang lebih baik dimana masing-masing memiliki nilai R^2 yaitu sebesar -1.880080745581838 dan -2.432728538383974.

Secara lebih jauh perbandingan Model 1, 2, 3, dan 4 bisa dilihat pada Gambar 4 berikut.

![download (1)](https://github.com/ahmadsuaif/Proyek-Pertama-Predictive-Analytics/assets/66425290/a46a2fa1-d5c5-4371-a18f-409a84bb42da)

Gambar 4. Perbandingan Model berdasarkan Nilai Error (dalam 1e6)

Berdasarkan Gambar 4 dapat terlihat bahwa nilai error train dan test dari Model 3 (RF1) dan Model 4 (RF2) jauh lebih baik dibandingkan model lainnya.

Selain itu dilakukan perbandingan nilai y_true terhadap nilai prediksi harga rumah dari 4 buah model yang dibuat. Tabel 2 berikut merupakan hasil dari evaluasi model yang telah dibuat.

|     |y_true|prediksi_LR|prediksi_RR|prediksi_RF1|prediksi_RF2|
|---|---|---|---|---|---|
|15732|341700|218287.6|218309.3|347466.0|315645.2|

Tabel 2. Perbandingan Model


Berdasarkan hasil evaluasi, terlihat bahwa prediksi harga rumah dengan *Random Forest* (RF), baik RF1 (tanpa tuning) ataupun RF2 (dengan tuning) memberikan hasil yang paling mendekati y_true, dimana nilai y_true yaitu 341700 dan nilai RF1 dan RF2 masing-masing yaitu 347466.0 dan 315645.2. Dengan demikian bisa disimpulkan bahwa model yang telah dikembangkan dapat memprediksi harga rumah dengan baik dengan menggunakan *Random Forest Regressor*.

## Referensi:
[1] Akhlak, Nancy, Suchit, Anil. (2021). Play Store App Analysis. International Research Journal of Engineering and Technology. 8. 3888-3893.

[2] Burke, Robin & Felfernig, Alexander & Göker, Mehmet. (2011). Recommender Systems: An Overview. Ai Magazine. 32. 13-18. 10.1609/aimag.v32i3.2361. 

[3] Pagare, Reena & Shinde, Anita. (2012). A Study of Recommender System Techniques. International Journal of Computer Applications. 47. 1-4. 10.5120/7269-0078. 

[4] Cremonesi, Paolo & Donatacci, A. & Garzotto, Franca & Turrin, R.. (2012). Decision-making in recommender systems: The role of user's goals and bounded resources. CEUR Workshop Proceedings. 893. 1-7.

[5] Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645. 
