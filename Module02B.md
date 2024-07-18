Modul 2B : Analisis Distribusi Spesies Menggunakan Data Bioklimat
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
data_path diatur ke lokasi spesifik pada drive komputer. Di sini, "D:/05_Research/08_Biodiversity/Maxent/" adalah direktori di mana data dan file terkait disimpan. Path ini harus disesuaikan dengan struktur direktori di mana pengguna menyimpan file proyek mereka. Menggunakan drive D:/ menunjukkan bahwa data disimpan di partisi atau drive sekunder, yang sering digunakan untuk data penelitian atau proyek besar yang memerlukan penyimpanan yang terpisah dari sistem operasi utama.

