# Modul 2B : Analisis Distribusi Spesies Menggunakan Data Bioklimat
--------------

Modul ini dirancang untuk membekali peserta dengan keterampilan dan pengetahuan yang diperlukan untuk mengumpulkan, mengolah, dan menganalisis data bioklimat dan kejadian spesies guna memodelkan distribusi spesies. Peserta akan belajar menggunakan berbagai paket di R untuk mengelola data lingkungan besar, melaksanakan analisis statistik, serta melakukan prediksi distribusi spesies saat ini dan masa depan berdasarkan skenario perubahan iklim.


## 1. PENGATURAN LINGKUNGAN KERJA
Dalam modul pelatihan ini, langkah pertama yang sangat penting adalah pengaturan direktori kerja yang efisien dan efektif. Pengaturan direktori kerja dalam R adalah krusial karena menentukan di mana file-file data akan disimpan dan diakses, dan juga di mana hasil output akan ditempatkan. Proses ini memastikan bahwa semua file yang diperlukan dapat ditemukan dan diakses oleh script R dengan mudah tanpa harus menyertakan path lengkap setiap kali mengakses file tersebut.

### Penentuan Path
Dalam skrip yang diberikan:

```
r
Copy code
data_path = "D:/05_Research/08_Biodiversity/Maxent/"
setwd(data_path)
```
data_path diatur ke lokasi spesifik pada drive komputer. Di sini, ```"D:/05_Research/08_Biodiversity/Maxent/"``` adalah direktori di mana data dan file terkait disimpan. Path ini harus disesuaikan dengan struktur direktori di mana pengguna menyimpan file proyek mereka. Menggunakan drive D:/ menunjukkan bahwa data disimpan di partisi atau drive sekunder, yang sering digunakan untuk data penelitian atau proyek besar yang memerlukan penyimpanan yang terpisah dari sistem operasi utama.

### Menggunakan Path Relatif
Menggunakan path absolut, seperti yang terlihat di atas, dapat menyebabkan masalah ketika skrip dibagikan dengan orang lain yang mungkin tidak memiliki struktur folder yang sama. Sebagai alternatif, path relatif dapat lebih fleksibel. Misalnya, jika skrip R dan data disimpan dalam folder yang sama, Anda bisa menggunakan ```setwd("./data/") ``` untuk merujuk ke subfolder data di direktori saat ini di mana skrip R dijalankan. Ini meningkatkan portabilitas skrip, membuatnya lebih mudah untuk digunakan oleh orang lain pada sistem yang berbeda.

### Meminta Pengguna Menentukan Direktori
Alternatif lain adalah meminta pengguna untuk menentukan direktori saat skrip dijalankan. Ini dapat dilakukan dengan menggunakan fungsi seperti ```choose.dir()``` pada Windows atau ```file.choose()``` yang memungkinkan pengguna memilih direktori melalui dialog file. Ini adalah pendekatan yang user-friendly terutama ketika mendistribusikan skrip ke audiens yang lebih luas yang mungkin tidak nyaman dengan pengeditan kode.

## 2. MANAJEMEN LIBRARY
Dalam konteks pengolahan data dan analisis menggunakan R, sangat penting untuk memastikan bahwa semua paket yang diperlukan terinstal dan siap digunakan sebelum menjalankan skrip. Fungsi ensurePackages dalam skrip Anda dirancang untuk mengotomatisasi proses ini, sehingga meningkatkan efisiensi dan mengurangi kemungkinan kesalahan saat menjalankan analisis. Berikut adalah penjelasan terperinci tentang bagaimana fungsi ini bekerja dan manfaatnya dalam pengembangan skrip R.

### Fungsi ensurePackages
Fungsi ensurePackages bertujuan untuk memastikan bahwa semua paket yang diperlukan untuk skrip Anda sudah terinstal dan terload ke sesi R saat ini. Ini mengurangi risiko menghadapi error karena kekurangan paket saat skrip dijalankan.

```
ensurePackages <- function(packages) {
    # Identifikasi paket yang belum terinstal
    new_packages <- packages[!packages %in% rownames(installed.packages())]
    # Instalasi paket yang belum terinstal
    if(length(new_packages) > 0) {
        install.packages(new_packages)
    }
    # Memuat semua paket yang ditentukan menggunakan sapply untuk pemrosesan batch
    sapply(packages, require, character.only = TRUE)
}
```
### Langkah-langkah Fungsi
 1.  **Identifikasi Paket yang Belum Terinstal:** Fungsi memulai dengan membuat daftar ```new_packages``` yang mengandung nama-nama paket dari argumen ```packages``` yang belum terinstal di mesin pengguna. Ini dilakukan dengan membandingkan daftar packages dengan paket yang sudah terinstal, yang didapat dari ```installed.packages()```.
 2.  **Instalasi Paket:** Jika ada paket yang belum terinstal ```(length(new_packages) > 0)```, fungsi akan secara otomatis menginstal paket-paket tersebut menggunakan ```install.packages()```.
 3.  **Memuat Paket:** Terakhir, fungsi menggunakan ```sapply()``` untuk memuat paket-paket yang telah diinstal. ```sapply()``` memudahkan proses ini dengan menerapkan fungsi ```require``` secara batch kepada setiap elemen dari vektor ```packages```, yang mengimpor paket-paket tersebut ke sesi R.

### Manfaat
 1.  **Otomatisasi:** Otomatisasi pemasangan dan pemuatan paket menghemat waktu dan mengurangi kesalahan manusia.
 2.  **Keandalan:** Meningkatkan keandalan skrip dengan memastikan semua dependensi terpenuhi sebelum eksekusi.
 3.  **Portabilitas:** Mempermudah distribusi skrip kepada pengguna lain tanpa perlu pemasangan manual paket.

### Daftar Paket yang Diperlukan
Skrip Anda mencakup paket-paket berikut sebagai bagian dari analisis:

```
packages <- c("terra", "caret", "rsample", "sf", "dismo", "dplyr", "randomForest", "kernlab", "stats", "gam", "mgcv", "gbm", "tree", "mda", "ggplot2", "sdm", "sdmpredictors", "usdm", "stringr", "mapview", "raster", "geodata")
```
Setiap paket ini memiliki peran spesifik dalam analisis, seperti pemodelan, visualisasi, dan manipulasi data.
Dengan menggunakan pendekatan sistematis dalam mengelola paket, Anda memastikan bahwa skrip Anda siap untuk dijalankan di berbagai lingkungan dengan sedikit hambatan, memudahkan kerja kolaboratif dan reproduktivitas dalam penelitian.

### Memastikan Semua Paket Terinstal dan Terload
Bagian terakhir dari fungsi ensurePackages ini adalah memastikan bahwa semua paket yang telah diidentifikasi sebelumnya sebagai diperlukan benar-benar terinstal dan terload dalam sesi R Anda. Ini adalah langkah penting untuk mempersiapkan lingkungan eksekusi skrip sehingga semua fungsionalitas yang diperlukan tersedia tanpa masalah saat skrip dijalankan.

```
# Pastikan semua paket terinstal dan terload
ensurePackages(packages)
```
Langkah Eksekusi

 * **Panggilan Fungsi:** Pada baris kode ini, ensurePackages dipanggil dengan argumen packages, yang merupakan vektor yang berisi nama-nama paket yang diperlukan untuk analisis Anda.
 * **Pengaktifan Fungsi:** Fungsi ensurePackages kemudian melakukan iterasi melalui daftar paket. Untuk setiap paket, fungsi ini akan memeriksa apakah paket tersebut sudah terinstal. Jika belum, fungsi akan menginstal paket tersebut. Setelah instalasi, fungsi menggunakan require() untuk memuat paket, memastikan bahwa semua fungsionalitas dari paket tersebut tersedia untuk digunakan dalam skrip Anda.

Keuntungan Menjalankan Langkah Ini

 * **Kemudahan Penggunaan:** Dengan memastikan bahwa semua paket diinstal dan dimuat sebelum melanjutkan, Anda mengurangi risiko menghadapi error yang terkait dengan paket yang hilang atau belum dimuat saat menjalankan bagian kode selanjutnya.
 * **Otomatisasi Proses:** Proses ini otomatis, yang mengurangi beban konfigurasi manual dan memungkinkan Anda fokus pada analisis data.
 * **Konsistensi Lingkungan:** Memastikan lingkungan kerja yang konsisten di mana skrip dijalankan, yang sangat penting dalam konteks penelitian yang sering membutuhkan reproduksi hasil.

Integrasi baris kode ini sebelum proses analisis dimulai adalah praktek yang baik dalam scripting dan pengembangan software, memastikan bahwa skrip Anda dapat dijalankan dengan lancar dalam setiap eksekusi. Ini adalah elemen penting dari pengembangan skrip yang robust dan andal, memastikan bahwa semua dependensi teknis terpenuhi sebelum tugas inti dilakukan.

## 3. PERSIAPAN DATA BIOKLIMAT
Dalam modul analisis distribusi spesies, persiapan data bioklimat adalah langkah krusial yang melibatkan pengambilan, pemrosesan, dan analisis awal data untuk memastikan kualitas dan relevansi informasi yang digunakan dalam model prediktif. Langkah-langkah yang terlibat dalam proses ini, seperti yang diilustrasikan dalam skrip R anda, meliputi pengambilan data dari sumber terpercaya, pengurangan dimensi data, dan penyesuaian data terhadap skenario iklim masa depan.

### Pengambilan Data Bioklimat dari WorldClim
Skrip Anda mencakup paket-paket berikut sebagai bagian dari analisis:

```
# Mengambil variabel bioklimat dari WorldClim dengan resolusi 10 arc-menit
bio <- worldclim_global(res = 10, var = "bio", path = data_path)
bio <- raster::stack(bio)  # Menumpuk raster untuk memudahkan pengolahan
```
Di sini, ```worldclim_global``` digunakan untuk mengambil data variabel bioklimat dari basis data WorldClim. Resolusi data diatur pada 10 arc-menit, yang memberikan detail yang cukup untuk banyak aplikasi ekologis. Fungsi ```raster::stack``` kemudian digunakan untuk menggabungkan lapisan raster individu menjadi satu tumpukan yang dapat dikelola lebih lanjut.

### Konversi Raster ke DataFrame untuk Perhitungan VIF
```
# Konversi data raster ke data frame untuk kalkulasi VIF
bio_df <- as.data.frame(values(bio), xy = TRUE)  # Menghindari kelebihan memori
bio_df <- na.omit(bio_df)  # Menghilangkan nilai NA
```

Data raster dikonversi ke format data frame untuk memfasilitasi analisis statistik lebih lanjut. Menggunakan ```values()``` membantu menghindari masalah kelebihan memori yang sering terjadi saat bekerja dengan raster besar.

### Perhitungan dan Seleksi Variabel dengan VIF
```
# Menghitung VIF dan mengeksklusi lapisan dengan korelasi tinggi
vif_results <- vifcor(bio_df[, -c(1,2)])  # Kolom pertama dan kedua biasanya adalah koordinat
vif_to_exclude <- vif_results@excluded  # Menggunakan threshold yang telah ditentukan
names_to_exclude <- names(bio)[vif_to_exclude]
biom <- subset(bio, !(names(bio) %in% names_to_exclude))
```

Variabel Inflation Factor (VIF) digunakan untuk mengidentifikasi dan mengeksklusi variabel yang memiliki korelasi tinggi yang bisa mengganggu analisis. Data yang memiliki VIF tinggi dikecualikan dari analisis lebih lanjut untuk meningkatkan keandalan model prediktif.

### Pengambilan dan Penyesuaian Data Bioklimat Masa Depan
```
# Mengambil data bioklimat masa depan berdasarkan skenario RCP 8.5 dari model CMIP5
biof <- cmip6_world("CNRM-CM6-1", "585", "2061-2080", var="bioc", res=10, path = data_path)
biof <- raster::stack(biof)
biof <- biof[[!names(biof) %in% names(biof)[vif_to_exclude]]]
names(biof) <- names(bio)
```

Data bioklimat masa depan diambil dari model CMIP6 dengan skenario RCP 8.5, yang menggambarkan proyeksi iklim di masa depan berdasarkan asumsi tertentu tentang emisi gas rumah kaca. Data ini juga disesuaikan untuk memastikan konsistensi dengan set data historis.

### Penentuan dan Penyesuaian Ekstensi Geografis
```
# Mendefinisikan dan menyesuaikan ekstensi geografis untuk area studi
study_extent <- extent(92.5154, 154.0976, -13.71008, 10.08345)
biom <- crop(biom, study_extent)
biof <- crop(biof, study_extent)
```

Ekstensi geografis area studi ditentukan, dan data bioklimat dipotong untuk membatasi analisis hanya pada area yang relevan. Ini memastikan bahwa model prediktif dibangun hanya berdasarkan data dari lokasi yang relevan.

## 4. PENGAMBILAN DATA KEJADIAN SPESIES
Proses pengambilan dan persiapan data kejadian spesies adalah langkah penting dalam analisis distribusi spesies. Langkah ini melibatkan mengumpulkan data dari sumber terpercaya dan mengintegrasikannya dengan data lingkungan untuk analisis yang lebih mendalam. Dalam kasus ini, data untuk spesies **Leucopsar rothschildi** diambil dari Global Biodiversity Information Facility (GBIF).

### Pengambilan Data dari GBIF
```
species_names <- c("Leucopsar rothschildi")
sp <- gbif(genus = "Leucopsar", species = "rothschildi", download = TRUE, geo = TRUE, sp = FALSE) %>%
  filter(!is.na(lon)) %>%
  mutate(species = 1) %>%
  select(lon, lat, species) %>%
  st_as_sf(coords = c("lon", "lat"), crs = 4326) %>%
  st_crop(study_extent)
```
Langkah-langkah dalam pengambilan data:

 1. **Pengambilan Data:** Data diambil menggunakan fungsi ```gbif()``` yang secara spesifik mencari genus dan spesies yang ditargetkan.
 2. **Pembersihan Data:** Data dibersihkan untuk menghilangkan nilai yang tidak memiliki koordinat (```lon```), yang esensial untuk analisis spasial.
 3. **Transformasi Data:** Data ditransformasi ke format ```sf``` (simple features), yang merupakan format yang efisien untuk analisis geospasial dalam R.
 4. **Pemotongan Data:** Data dipotong sesuai dengan ```study_extent``` untuk memastikan bahwa hanya data dalam area studi yang dijaga.

### Integrasi Data Lingkungan
```
{
  .data <- .
  environmental_values <- extract(biom, .data)
  environmental_df <- as.data.frame(environmental_values)
  combined_data <- cbind(.data, environmental_df)
}
sp <- as(sp, 'Spatial')
```
Setelah data kejadian spesies siap, nilai lingkungan dari raster bioklimatik diekstrak untuk setiap titik kejadian. Data ini kemudian digabungkan dengan data kejadian spesies untuk membuat satu set data yang mencakup informasi lokasi dan kondisi lingkungan.

### Visualisasi Data Kejadian Spesies
```
plot(biom[[2]])  # Plotting one of the bioclimatic layers
points(sp, cex = 0.5, pch = 16)  # Plotting species occurrence points
```
Langkah terakhir adalah visualisasi. Lapisan bioklimatik diplot sebagai latar belakang, dan titik-titik kejadian spesies ditambahkan sebagai overlay. Ini memberikan representasi visual dari distribusi spesies relatif terhadap faktor lingkungan yang dipilih, yang sangat berguna untuk analisis awal distribusi spesies dan identifikasi pola atau anomali.

## 5. MODELING DISTRIBUSI SPESIES
Proses pemodelan distribusi spesies menggunakan data yang telah dikumpulkan dan dipersiapkan memberikan insight penting tentang bagaimana spesies tersebar di seluruh wilayah studi, dan bagaimana faktor lingkungan mempengaruhi distribusi mereka. Dalam tahap ini, berbagai metode pemodelan diterapkan untuk membangun model prediktif yang kuat.

### Persiapan Data untuk Pemodelan
```
d <- sdmData(formula = species ~ ., train = sp, predictors = biom, bg = list(n=1000, method = 'gRandom'))
```

Data disiapkan dengan fungsi ```sdmData```, yang mengintegrasikan data kejadian spesies (```sp```) dan data prediktor bioklimatik (```biom```). Dalam persiapan ini, juga ditentukan background (```bg```) sampling dengan 1000 titik yang dihasilkan secara acak (```gRandom```), yang diperlukan untuk teknik pemodelan seperti MaxEnt.

### Menjalankan Model Distribusi Spesies
```
m <- sdm::sdm(species ~ ., d, methods = c('glm', 'svm', 'rf'), replication = c('cv', 'boot'), cv.folds = 5, n = 10)
gui(m)
```

Beberapa algoritma digunakan untuk pemodelan, termasuk Regresi Logistik Generalisasi (```glm```), Mesin Vektor Pendukung (```svm```), dan Random Forest (```rf```). Model-model ini dijalankan dengan validasi silang dan bootstrapping untuk memperkuat validitas model. GUI (```gui(m)```) dapat digunakan untuk memvisualisasikan dan membandingkan performa dari masing-masing model.

### Prediksi dan Visualisasi Distribusi Saat Ini
```
current_pred <- predict(m, biom, paste(species_names, "predictions.img", sep = ""), mean = TRUE, overwrite = TRUE)
plot(current_pred)
```

Setelah model-model tersebut dilatih, mereka digunakan untuk memprediksi distribusi spesies saat ini menggunakan data bioklimatik yang sama yang digunakan selama pelatihan. Hasilnya divisualisasikan untuk memberikan gambaran geografis tentang probabilitas keberadaan spesies di wilayah studi.

### Pemodelan Ensemble untuk Kondisi Saat Ini
```
current_ens <- ensemble(m, biom, paste(species_names, "ens.img", sep = ""), setting = list(method = 'weights', stat = "TSS", opt = 2))
plot(current_ens)
```

Model ensemble digunakan untuk menggabungkan prediksi dari berbagai model individual untuk meningkatkan keakuratan dan stabilitas prediksi. Metode 'weights' digunakan di sini, dengan menggunakan statistik ```True Skill Statistic (TSS)``` untuk mengoptimalkan bobot. Ensemble ini memberikan estimasi yang lebih robust terhadap distribusi spesies saat ini, memanfaatkan kekuatan dari masing-masing model yang dijalankan.

Tahapan ini mengakhiri proses pemodelan distribusi spesies dengan menyediakan berbagai metode prediktif yang memungkinkan peneliti dan praktisi untuk mengidentifikasi faktor lingkungan kunci dan potensi perubahan distribusi spesies dalam respons terhadap perubahan tersebut. Setiap langkah dirancang untuk memastikan bahwa model yang dihasilkan tidak hanya statistik yang kuat tetapi juga relevan dan mudah diinterpretasikan dalam konteks ekologis.

## 6. PREDIKSI DISTRIBUSI SPESIES MASA DEPAN DI BAWAH SKENARIO PERUBAHAN IKLIM
Dalam menghadapi perubahan iklim, memprediksi bagaimana distribusi spesies mungkin berubah menjadi sangat penting untuk konservasi dan manajemen sumber daya. Langkah ini menggunakan model yang telah dikembangkan untuk memproyeksikan distribusi spesies di masa depan berdasarkan skenario iklim yang diubah.

### Prediksi Distribusi Masa Depan
```
future_pred <- predict(m, biof, paste(species_names, "predictionsf.img", sep = ""), overwrite = TRUE)
```

Prediksi ini menggunakan model yang telah dilatih (```m```) dan data bioklimatik masa depan (```biof```) yang diambil dari skenario RCP 8.5 model CMIP5. Hasil ini memberikan gambaran tentang bagaimana kondisi habitat spesies mungkin berubah, yang akan mempengaruhi keberadaan dan sebaran spesies tersebut.

### Pemodelan Ensemble untuk Kondisi Masa Depan
```
future_ens <- ensemble(m, biof, paste(species_names, "ensf.img", sep = ""), overwrite = TRUE, setting = list(method = 'weights', stat = "TSS", opt = 2))
plot(future_ens)
```

Pemodelan ensemble diimplementasikan untuk memperkuat keandalan prediksi masa depan. Seperti pada prediksi saat ini, model ini mengintegrasikan hasil dari berbagai model untuk menghasilkan prediksi yang lebih stabil dan dapat diandalkan. Pengaturan ini menggunakan bobot berbasis ```True Skill Statistic (TSS)```, yang memberikan indikasi kinerja model yang baik dalam kondisi variabel yang diubah.


### Pengaturan Ambang Batas pada Prediksi Ensemble
Fungsi untuk mengatur ambang batas pada prediksi ensemble membantu dalam mengkategorikan area sebagai cocok atau tidak cocok untuk spesies berdasarkan nilai probabilitas tertentu.
```
threshold_ensemble <- function(ensemble, threshold = 0.4) {
    ensemble[ensemble >= threshold] <- 1
    ensemble[ensemble < threshold] <- NA
    return(ensemble)
}
```

Fungsi ini menetapkan area di mana probabilitas keberadaan spesies di atas ambang tertentu sebagai 'cocok' (1) dan yang lainnya sebagai 'tidak cocok' (NA), yang membantu dalam visualisasi dan analisis lebih lanjut.

### Aplikasi Pengaturan Ambang dan Visualisasi
Fungsi untuk mengatur ambang batas pada prediksi ensemble membantu dalam mengkategorikan area sebagai cocok atau tidak cocok untuk spesies berdasarkan nilai probabilitas tertentu.
```
current_ens1 <- threshold_ensemble(current_ens)
future_ens1 <- threshold_ensemble(future_ens)

plot(current_ens1)
plot(future_ens1)
mapview(stack(current_ens1, future_ens1))
```

Penerapan ambang batas pada prediksi saat ini dan masa depan memungkinkan visualisasi yang jelas tentang area yang mungkin kehilangan atau memperoleh kecocokan habitat sebagai akibat dari perubahan iklim. Fungsi mapview digunakan untuk menampilkan kedua set prediksi secara bersamaan, memberikan visualisasi interaktif yang dapat membantu dalam memahami dampak spatial dari perubahan yang diproyeksikan.

Langkah-langkah ini memberikan kerangka kerja untuk mengkaji dan memvisualisasikan potensi perubahan distribusi spesies di bawah pengaruh perubahan iklim, sangat berguna bagi peneliti, pengambil kebijakan, dan praktisi konservasi dalam merencanakan strategi adaptasi dan mitigasi.




