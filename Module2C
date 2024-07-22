## 1. PENGATURAN LINGKUNGAN KERJA
Dalam modul pelatihan ini, langkah pertama yang sangat penting adalah pengaturan direktori kerja yang efisien dan efektif. Pengaturan direktori kerja dalam R adalah krusial karena menentukan di mana file-file data akan disimpan dan diakses, dan juga di mana hasil output akan ditempatkan. Proses ini memastikan bahwa semua file yang diperlukan dapat ditemukan dan diakses oleh script R dengan mudah tanpa harus menyertakan path lengkap setiap kali mengakses file tersebut.

### Penentuan Path
Dalam skrip yang diberikan:

```
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

PENGAMBILAN DATA KEJADIAN SPESIES
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
plot(  # Plotting one of the bioclimatic layers
points(sp, cex = 0.5, pch = 16)  # Plotting species occurrence points
)
```
Langkah terakhir adalah visualisasi. Lapisan bioklimatik diplot sebagai latar belakang, dan titik-titik kejadian spesies ditambahkan sebagai overlay. Ini memberikan representasi visual dari distribusi spesies relatif terhadap faktor lingkungan yang dipilih, yang sangat berguna untuk analisis awal distribusi spesies dan identifikasi pola atau anomali.
