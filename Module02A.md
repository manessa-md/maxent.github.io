# Modul 2A : Dasar Bahasa Pemrograman R
---
## 1. PENGENALAN R DAN RSTUDIO
---
### 1.1 Pengenalan ke R

#### Sejarah dan Kegunaan R:

R adalah sebuah bahasa pemrograman dan lingkungan statistik yang banyak digunakan oleh statistisi, data scientist, dan peneliti untuk analisis data dan pengembangan perangkat lunak statistik. R dikembangkan oleh Ross Ihaka dan Robert Gentleman di University of Auckland, New Zealand, dan kini dikelola oleh R Core Team. R merupakan implementasi dari bahasa S yang diciptakan di Bell Laboratories. R dirilis pertama kali pada tahun 1995, dan menjadi populer karena kemampuannya yang luas dalam statistik terapan dan grafik data yang kaya.
Kegunaan R mencakup:

• Analisis statistik data

• Pembuatan grafik secara grafis

• Pengolahan dan manipulasi data

• Pembuatan perangkat lunak statistik

• Machine learning

#### Instalasi R dan RStudio:

Untuk menginstal R dan RStudio, ikuti langkah-langkah berikut:

#### 1.	Menginstal R:
   • Kunjungi website CRAN (Comprehensive R Archive Network) di https://cran.r-project.org.
 
   • Pilih versi sesuai dengan sistem operasi yang Anda gunakan (Windows, Mac, atau Linux).
  
   • Download dan jalankan installer.
 
 #### 2.	Menginstal RStudio:
 
  • Kunjungi website RStudio di https://rstudio.com dan pilih RStudio Desktop.

  • Pilih versi RStudio yang sesuai dengan sistem operasi Anda.

  • Download dan instal RStudio setelah R terinstal.


### 1.2 Mengenal RStudio
#### Antarmuka RStudio:

RStudio menyediakan antarmuka yang user-friendly untuk penggunaan R yang efektif. Antarmuka utama RStudio terdiri dari empat panel:

  •	**Console**: Tempat Anda menulis dan menjalankan kode R.
  
  •	**Script**: Editor teks tempat Anda menulis skrip yang dapat disimpan dan dijalankan ulang.
  
  •	**Environment/History**: Menampilkan variabel yang aktif dalam memori dan riwayat kode yang telah dijalankan.
  
  •	**Files/Plots/Packages/Help/Viewer**: Tab yang berguna untuk navigasi file, melihat grafik, mengelola paket, mendapatkan bantuan, dan lainnya.
  
Penggunaan Dasar RStudio:
#### 1.	Console:

• Tempat untuk eksperimen cepat dengan kode.

• Jalankan perintah secara langsung dan lihat outputnya.

#### 2.	Script:
•	Buat skrip baru dengan File > New File > R Script.

•	Tulis kode yang bisa dijalankan secara berulang.

• Jalankan kode dari skrip ke console dengan menekan Ctrl+Enter (Cmd+Enter di Mac).

#### 3.	Environment/History:
•	**Environment**: Lihat daftar objek (variabel, fungsi) yang telah Anda buat.

•	**History**: Lihat dan ulangi perintah yang telah Anda jalankan sebelumnya.

#### 4.	Files/Plots/Packages/Help/Viewer:
•	**Files**: Navigasi dan kelola file dari RStudio.

•	**Plots**: Lihat plot yang dihasilkan oleh kode R.

--- 
## 2: TIPE DATA DAN STRUKTUR DATA
---
### 2.1 Tipe Data Dasar

Numeric, Character, Logical:

•	**Numeric**: Ini adalah tipe data yang digunakan untuk menyimpan angka, yang bisa berupa bilangan bulat atau desimal (contoh: 5, 20, 3.1416).

•	**Character**: Tipe data untuk menyimpan teks. Setiap nilai karakter harus ditempatkan dalam tanda kutip (contoh: "Hello", "R").

•	**Logical**: Tipe data ini hanya memiliki dua nilai, TRUE atau FALSE, yang digunakan untuk logika kondisional dan pengendalian alur.

Vektor, Matriks, dan Array:

•	**Vektor**: Koleksi elemen tipe data yang sama. Dalam R, vektor bisa dibuat menggunakan fungsi _c()_. Contoh: c(1, 2, 3, 4) untuk numeric atau c("a", "b", "c") untuk character.

•	**Matriks**: Struktur data dua dimensi, dimana setiap elemen harus memiliki tipe data yang sama. Matriks bisa dibuat dengan fungsi_ matrix()_.

•	**Array**: Versi yang lebih umum dari matriks yang bisa memiliki lebih dari dua dimensi. Array dibuat dengan fungsi array().

•	**Packages**: Kelola paket-paket R, instalasi, dan update.

•	**Help**: Akses dokumentasi untuk fungsi R.

•	**Viewer**: Tampilkan konten HTML, PDF, dan lainnya.

### 2.2 Struktur Data Kompleks
Data Frames dan Lists:

•	**Data Frames**: Mungkin merupakan struktur data paling penting di R yang digunakan untuk menyimpan data tabel. Setiap kolom dalam data frame bisa memiliki tipe data yang berbeda (numeric, character, logical, dll), mirip dengan spreadsheet. Data frame dibuat dengan fungsi _data.frame()_.

•	**Lists**: Koleksi elemen yang bisa memiliki tipe data dan panjang yang berbeda. List bisa menyimpan kombinasi dari berbagai struktur data lain, termasuk vektor, matriks, data frames, dan bahkan list lainnya. List dibuat dengan fungsi _list()._

Faktor dan Tabel:

•	**Faktor**: Digunakan untuk menyimpan data kategorikal. Faktor memiliki tingkat atau label yang menunjukkan kategori dari data tersebut. Misalnya, faktor untuk jenis kelamin bisa memiliki dua label, "Male" dan "Female". Faktor dibuat dengan fungsi _factor()_.
•	**Tabel**: Sering digunakan untuk membuat tabulasi silang dari data. Ini bisa sangat berguna untuk analisis data eksplorasi. Tabel dibuat menggunakan fungsi _table()._
