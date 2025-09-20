### **Analisis Keluhan Pelanggan Tokopedia: Klasifikasi Topik dan Ringkasan Otomatis Menggunakan AI IBM Granite**

### **Project Overview**
Setiap harinya, platform *e-commerce* seperti Tokopedia menerima ribuan ulasan produk dari pelanggan. Di antara ulasan tersebut, ulasan negatif (dengan rating rendah) mengandung informasi krusial mengenai masalah yang dihadapi pelanggan, mulai dari kualitas produk, proses pengiriman, hingga pelayanan penjual. Menganalisis keluhan ini secara manual untuk menemukan akar masalah adalah proses yang lambat, tidak efisien, dan sulit untuk diskalakan.

Proyek ini bertujuan untuk mengatasi tantangan tersebut dengan memanfaatkan *Large Language Model* (LLM), yaitu IBM Granite. Kami mengembangkan sebuah alur kerja untuk secara otomatis:
1.  **Mengklasifikan** setiap ulasan negatif ke dalam kategori keluhan yang spesifik.
2.  **Membuat ringkasan** cerdas dari kumpulan keluhan per kategori untuk menyajikan *insight* utama dengan cepat.

Dengan pendekatan ini, tim produk dan bisnis dapat dengan mudah memahami titik masalah utama yang dialami pelanggan dan mengambil tindakan perbaikan yang lebih tepat sasaran.

---
### **Dataset Link** 
Link Dataset: https://www.kaggle.com/datasets/farhan999/tokopedia-product-reviews?resource=download 

---

### **Insight & Findings (Temuan Utama)**
Berdasarkan analisis terhadap 100 sampel ulasan negatif (rating 1 & 2), kami menemukan beberapa pola keluhan yang dominan:


1.  **Masalah Paling Umum adalah "Tidak Sesuai Deskripsi" dan "Kualitas Produk"**: Dari sampel yang dianalisis, mayoritas keluhan pelanggan berpusat pada dua isu utama. Ini menandakan adanya kesenjangan antara ekspektasi yang diciptakan oleh halaman produk (gambar, deskripsi, judul) dengan realitas produk yang diterima pelanggan.

2.  **Isu Kualitas Merujuk pada Kerusakan dan Fungsionalitas**: Ringkasan AI menunjukkan bahwa keluhan "Kualitas Produk" tidak hanya soal bahan yang jelek, tetapi juga tentang produk yang **rusak, cacat, atau tidak berfungsi** sama sekali (misalnya, staples yang tidak bekerja).  Hal ini mengindikasikan perlunya peningkatan kontrol kualitas (QC) sebelum pengiriman.

3.  **Pengiriman yang Lambat Menjadi Sumber Frustrasi**: Untuk kategori "Pengiriman", masalah utama adalah **keterlambatan** dan **kurangnya komunikasi** dari penjual terkait status pengiriman.  Pelanggan merasa prosesnya tidak efisien dan respons penjual sangat lambat.

4.  **Pelayanan Penjual yang Kurang Responsif**: Keluhan pada kategori "Pelayanan Penjual" secara spesifik menyoroti penjual yang **tidak membalas chat**, **tidak teliti** dalam menyiapkan pesanan (item kurang), dan **tidak memberikan solusi** yang memuaskan ketika terjadi masalah. 

---

### **Conclusion & Recommendation (Kesimpulan & Rekomendasi)**
**Kesimpulan:**
Analisis menggunakan AI IBM Granite berhasil mengidentifikasi bahwa area masalah terbesar bagi pelanggan Tokopedia (berdasarkan sampel ulasan negatif) adalah **kualitas produk yang buruk** dan **ketidaksesuaian produk dengan deskripsi di etalase**. Masalah sekunder yang juga signifikan adalah **proses pengiriman yang lambat** dan **pelayanan penjual yang tidak responsif**.

**Rekomendasi:**
Berdasarkan temuan tersebut, berikut adalah rekomendasi yang dapat ditindaklanjuti:
1.  **Untuk Tim Penjual/Seller Tokopedia:**
    * **Tingkatkan Akurasi Halaman Produk**: Lakukan audit rutin pada deskripsi, foto, dan judul produk untuk memastikan semua informasi akurat dan sesuai dengan kondisi fisik barang.
    * **Perketat Quality Control (QC)**: Implementasikan prosedur pengecekan produk sebelum dikirim untuk meminimalkan jumlah barang rusak atau cacat yang sampai ke tangan pelanggan.
    * **Tingkatkan Standar Pelayanan**: Berikan pelatihan kepada penjual mengenai pentingnya komunikasi yang cepat, proaktif, dan solutif, terutama saat menangani keluhan.

2.  **Untuk Tim Platform Tokopedia:**
    * **Edukasi Penjual**: Buat program edukasi atau *workshop* bagi para penjual mengenai praktik terbaik dalam membuat deskripsi produk dan manajemen kualitas.
    * **Sistem Peringatan Kualitas**: Kembangkan fitur *dashboard* bagi penjual yang dapat memberikan peringatan jika produk mereka menerima banyak ulasan negatif terkait kualitas atau ketidaksesuaian deskripsi.

---

### **AI Support Explanation (Penjelasan Dukungan AI)**
Dalam proyek ini, model AI **IBM Granite (`ibm-granite/granite-13b-chat-v2`)** yang diakses melalui Replicate memainkan dua peran kunci:

1.  **Sebagai Classifier (Pengklasifikasi)**:
    * Kami merancang sebuah *prompt* yang menginstruksikan model untuk mengkategorikan setiap ulasan negatif ke dalam salah satu dari lima kategori yang telah ditentukan (*Kualitas Produk, Pengiriman, Pelayanan Penjual, Tidak Sesuai Deskripsi, Lainnya*).
    * Dengan memberikan aturan "HANYA berikan nama kategori", kami memaksa model untuk memberikan jawaban yang bersih dan terstruktur, yang kemudian dapat langsung dimasukkan ke dalam *dataframe* analisis kami.

2.  **Sebagai Summarizer (Peringkas)**:
    * Untuk setiap kategori keluhan, kami menggabungkan hingga 20 ulasan relevan menjadi satu teks besar.
    * Kami kemudian memberikan *prompt* kepada model AI untuk membaca kumpulan keluhan tersebut dan menyajikannya kembali dalam bentuk 2-3 poin ringkasan utama. Ini sangat efektif untuk mengekstrak inti masalah dari puluhan ulasan tanpa harus membacanya satu per satu.

Penggunaan AI secara signifikan mempercepat proses analisis dari yang tadinya memakan waktu berjam-jam (jika manual) menjadi hanya beberapa menit, serta menghasilkan *insight* yang tajam dan terstruktur.
