Langkah Kerja :

Buka zip kedua kumpulan data ke folder di komputer Anda. Di Panel Browser QGIS, temukan direktori tempat Anda mengekstrak data. Perluas ne_10m_landfolder dan pilih ne_10m_land.shplayer. Seret layer ke kanvas.

Anda akan mendapatkan layer baru ne_10m_land ditambahkan ke panel Layers. Basis data pembangkit listrik global hadir sebagai file CSV, jadi kita perlu mengimpornya. Klik tombol Buka Pengelola Sumber Data pada Bilah Alat Sumber Data. Anda juga dapat menggunakan pintasan keyboard Ctrl + L.

Di jendela Pengelola Sumber Data, alihkan ke tab Teks Dibatasi. Klik tombol ... di sebelah Nama file dan ramban ke direktori tempat Anda mengekstrak file globalpowerplantdatabasev120.zip. Pilih global_power_plant_database.csv. QGIS akan otomatis mendeteksi bidang pembatas dan geometri. Biarkan Geometry CRS ke nilai default EPSG:4326 - WGS84. Klik Tambah diikuti oleh Tutup.

A new layer global_power_plant_database will be added to the Layers panel and you will see the points representing the power plants in the canvas. Now we are ready to style both these layers. Click the Open the Layer Styling panel button at the top of the Layers panel.

Panel Layer Styling akan terbuka di sebelah kanan. Pilih layer ne_10m_land terlebih dahulu. Ini akan menjadi lapisan dasar kami sehingga kami dapat menjaga gaya minimalis agar tidak mengganggu. Klik Isi sederhana dan gulir ke bawah. Pilih warna Fill sesuai keinginan Anda. Klik drop-down di sebelah warna Stroke dan pilih Transparent Stroke. Ini akan mengatur garis besar poligon tanah menjadi transparan. Anda akan melihat hasil seleksi Anda diterapkan segera ke lapisan.

Selanjutnya pilih layer global_power_plant_database. Klik pada penanda Sederhana dan gulir ke bawah. Pilih penanda segitiga.

Gulir ke atas dan pilih warna Isi sesuai keinginan Anda. Teknik kartografi yang berguna adalah memilih versi warna isian yang sedikit lebih gelap sebagai warna Stroke. Daripada mencoba memilihnya secara manual, QGIS menyediakan ekspresi untuk mengontrol ini dengan lebih tepat. Klik tombol Penimpaan yang ditentukan data dan pilih Edit.

Masukkan ekspresi berikut untuk mengatur warna menjadi bayangan 30% lebih gelap dari warna isian dan klik OK. darker(@symbol_color, 130)

Anda akan melihat bahwa tombol Override yang ditentukan Data di sebelah Warna Stroke telah berubah menjadi kuning - menunjukkan bahwa properti ini dikendalikan oleh override. Render simbol tunggal dari lapisan pembangkit listrik tidak terlalu berguna. Itu tidak menyampaikan banyak informasi kecuali lokasi pembangkit listrik. Mari kita gunakan penyaji yang berbeda untuk membuatnya lebih berguna. Klik drop-down Symbology dan pilih Categorized renderer.

Lapisan global_power_plant_database berisi atribut yang menunjukkan bahan bakar utama yang digunakan di setiap pembangkit listrik. Kita dapat membuat gaya di mana setiap jenis bahan bakar yang unik ditampilkan dalam warna yang berbeda. Pilih primary_fuel sebagai Kolom. Klik Klasifikasi. Anda akan melihat beberapa kategori dan rendering peta berubah sesuai.

Meskipun tampilan Terkategori berguna, lapisan ini berisi terlalu banyak kategori untuk dapat ditafsirkan peta secara bermakna. Pendekatan yang lebih baik adalah mengelompokkan jenis kategori bahan bakar tertentu dan mengurangi jumlah kelas. Mari kita coba membuat 3 kategori - Bahan bakar terbarukan, Bahan bakar tidak terbarukan dan Lainnya. Pilih Perender berbasis aturan. Pilih semua kecuali satu aturan dengan menahan tombol Ctrl dan mengklik setiap baris. Setelah dipilih, klik tombol Hapus aturan yang dipilih untuk menghapusnya.

Pilih aturan yang tersisa dan klik Edit aturan saat ini.

Masukkan bahan bakar terbarukan sebagai Label. Klik tombol Ekspresi di sebelah Filter.

Dalam dialog Pembuat String Ekspresi, masukkan ekspresi berikut dan klik OK. Di sini kami mengelompokkan beberapa kategori energi terbarukan ke dalam satu kategori. "primary_fuel" IN ('Biomass', 'Geothermal', 'Hydro', 'Solar', 'Wind', 'Storage', 'Wave and Tidal')

Gulir ke bawah dan klik Penanda sederhana. Pilih warna Isi yang sesuai. Setelah selesai, klik tombol Kembali.

Anda akan melihat satu aturan diterapkan pada lapisan untuk kategori Renewable Fluel. Klik kanan baris dan pilih Salin. Klik kanan lagi dan pilih Tempel.

Salinan aturan yang ada akan ditambahkan. Pilih baris yang baru ditambahkan dan klik Edit aturan saat ini.

Masukkan Non-Renewable Fluel sebagai Label. Klik tombol Ekspresi di sebelah Filter.

Dalam dialog Pembuat String Ekspresi, masukkan ekspresi berikut dan klik OK. "primary_fuel" IN ('Coal', 'Gas', 'Nuclear', 'Oil', 'Petcoke')

Gulir ke bawah dan klik Penanda sederhana. Pilih warna Isi yang sesuai. Setelah selesai, klik tombol Kembali.

Ulangi proses Copy/Paste untuk menambahkan aturan ketiga. Pilih dan klik Edit aturan saat ini.

Masukkan Other sebagai Label. Pilih Lain - Tangkap semua untuk fitur lain, bukan Filter. Ini akan memastikan bahwa setiap kategori yang terlewatkan dalam 2 aturan sebelumnya, akan ditata oleh aturan ini. Gulir ke bawah dan klik Penanda sederhana. Pilih warna Isi yang sesuai. Setelah selesai, klik tombol Kembali.

Pengkategorian ulang selesai sekarang. Anda akan melihat tampilan yang jauh lebih bersih yang menunjukkan distribusi sumber bahan bakar terbarukan vs. tidak terbarukan yang digunakan oleh pembangkit listrik dan distribusinya di seluruh negara. Namun ini tidak memberikan gambaran yang lengkap. Kita bisa menambahkan variabel lain ke styling. Daripada menampilkan semua penanda dengan ukuran seragam, kami dapat menunjukkan ukuran yang proporsional dengan kapasitas pembangkit listrik masing-masing pembangkit. Teknik kartografi ini disebut pemetaan Multivariat. Klik kanan aturan Renewable Fluel dan pilih Ubah Ukuran.

Klik tombol Penimpaan yang ditentukan data di sebelah Ukuran. Pilih Sunting.

Karena kapasitas pembangkit listrik sangat bervariasi di antara kumpulan data kami, cara efektif untuk mendapatkan rentang ukuran yang kecil adalah menggunakan fungsi log10. Anda dapat bereksperimen dengan ekspresi yang berbeda untuk sampai pada apa yang terbaik untuk visualisasi pilihan Anda. Masukkan ekspresi berikut dan klik OK. log10("capacity_mw") + 1

Ulangi proses yang sama untuk aturan lainnya.

Setelah puas, Anda dapat menutup panel Layer Styling.

Melihat visualisasi akhir kami, Anda dapat langsung melihat pola di dataset. Sebagai contoh, di Eropa terdapat lebih banyak pembangkit listrik yang menggunakan sumber energi terbarukan, tetapi kapasitasnya lebih rendah daripada pembangkit yang menggunakan sumber energi tidak terbarukan.
 
