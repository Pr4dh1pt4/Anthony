# Anthony

Anthony ingin membuat sistem agar film-film favorit dia bisa lebih terorganisir dan mudah diakses. Anthony ingin melakukan beberapa hal dengan lebih efisien dan serba otomatis.

# 2️⃣ A
Anthony ingin semuanya serba instan dengan hanya satu perintah. Dengan satu perintah saja, Anthony bisa:
- Mendownload file ZIP yang berisi data film-film Netflix favoritnya.
- Mengekstrak file ZIP tersebut ke dalam folder yang sudah terorganisir.
- Menghapus file ZIP yang sudah tidak diperlukan lagi, supaya tidak memenuhi penyimpanan.

  **Fungsi log_message(const char* message)**

     ``` extension
     void log_message(const char* message) {
       FILE* log = fopen("log.txt", "a");
       if (!log) return;
   
       time_t now = time(NULL);
       struct tm *t = localtime(&now);
       fprintf(log, "[%02d:%02d:%02d] %s\n", t->tm_hour, t->tm_min, t->tm_sec, message);
       fclose(log);
 }
     - Fungsi ini mencatat pesan log ke dalam file log.txt dengan timestamp (jam:menit:detik).
     - Membantu dalam debugging dan pelacakan aktivitas program (misal: saat proses pengelompokan film berlangsung).

     
  **Fungsi parse_csv_line(char* line, char** fields, int max_fields)**

     ``` extension
     
     
  **Fungsi int extract_zip()**
     Deskripsi:
     Mengekstrak file netflixData.zip ke dalam folder data/ menggunakan pustaka libzip.
     
     Langkah-langkah:
     Membuka file ZIP.
     Membaca semua entri di dalam ZIP.
     Membuat direktori sesuai struktur file.
     Menulis isi file ZIP ke dalam sistem file.
     
     Kegunaan:
     Menyediakan file netflixData.csv yang dibutuhkan oleh proses selanjutnya.
     
  **Fungsi delete_zip()**
     Deskripsi:
     Menghapus file netflixData.zip dari sistem setelah berhasil diekstrak.
     
     Kegunaan:
     Menghemat ruang penyimpanan.
     
  **Fungsi void* menu_download(void* arg)**
     Deskripsi:
     Thread fungsi untuk menjalankan extract_zip() dan delete_zip().
     
     Kegunaan:
     Menyediakan antarmuka menu untuk pengguna melakukan ekstraksi file ZIP secara paralel.

# 2️⃣ B
Anthony ingin mengelompokkan film-filmnya dengan dua cara yang sangat mudah:
1. Berdasarkan huruf pertama dari judul film.
2. Berdasarkan tahun rilis (release year).

  *Langkah2 :*
  
  **Fungsi void* group_by_abjad(void* arg)**
  
     Deskripsi:
     Mengelompokkan film berdasarkan huruf pertama judul. Hasil disimpan dalam folder judul/ sesuai abjad atau simbol (#).
     
     Langkah-langkah:
     Membuka CSV dan membaca baris demi baris.
     Mendapatkan Title, Director, Year.
     Menyimpan hasil ke file judul/<A-Z/0-9/#>.txt.
 
     Kegunaan:
     Menyusun film agar mudah diakses berdasarkan inisial judul.
     
  **Fungsi void* group_by_year(void* arg)**
     Deskripsi:
     Mengelompokkan film berdasarkan tahun rilis dan menyimpannya ke dalam folder tahun/<year>.txt.
     
     Kegunaan:
     Menyediakan pengelompokan kronologis terhadap data film.
     
  **Fungsi void* menu_group(void* arg)**
     Deskripsi:
     Menjalankan thread untuk group_by_abjad dan group_by_year secara bersamaan.
     
     Kegunaan:
     Melakukan pengelompokan data film secara paralel demi efisiensi waktu.


# 2️⃣ C
Anthony ingin mengetahui statistik lebih mendalam tentang film-film yang dia koleksi. Misalnya, dia ingin tahu berapa banyak film yang dirilis *sebelum tahun 2000* dan *setelah tahun 2000*
  
  9. Fungsi void* generate_report(void* arg)
     Deskripsi:
     Membuat laporan statistik jumlah film berdasarkan Country, dibedakan antara film sebelum tahun 2000 dan setelah tahun 2000.
     
     Langkah-langkah:
     
     Baca dan parsing CSV.
     
     Hitung film per negara untuk dua periode waktu.
     
     Simpan ke file report_DDMMYYYY.txt.
     
     Kegunaan:
     Menyediakan laporan statistik untuk analisis atau dokumentasi.
     
 10. Fungsi void* menu_report(void* arg)
     Deskripsi:
     Menjalankan thread untuk fungsi generate_report().
     
     Kegunaan:
     Memanggil pembuatan laporan statistik melalui menu dengan thread terpisah.    
