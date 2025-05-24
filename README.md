# Laporan Proyek Machine Learning - Nadia Alzena Zahrani

# Domain Proyek

<h2>Latar Belakang</h2>
<p>
Tingkat putus kuliah (dropout) di perguruan tinggi merupakan permasalahan serius yang berdampak pada individu, institusi, dan masyarakat luas. Selain menyebabkan kerugian finansial dan psikologis bagi mahasiswa, tingginya angka dropout juga menurunkan reputasi institusi pendidikan dan efisiensi investasi pendidikan nasional. 
<br><br>
Menurut <i>Education Data Initiative</i>, hampir <b>40% mahasiswa di Amerika Serikat tidak menyelesaikan studinya hingga lulus</b>. Keputusan ini memiliki konsekuensi jangka panjang: mahasiswa yang drop out cenderung memiliki pendapatan sekitar <b>35% lebih rendah</b> dan menghadapi <b>risiko pengangguran 20% lebih tinggi</b> dibandingkan lulusan perguruan tinggi.
<br><br>
Oleh karena itu, upaya prediksi dan pencegahan dropout sangat penting untuk meningkatkan kualitas pendidikan dan daya saing bangsa.
</p>
<p>
Penelitian terkait prediksi dropout mahasiswa telah banyak dilakukan menggunakan pendekatan machine learning. Misalnya, Tamhane et al. (2014) menggunakan model prediksi berbasis data mining untuk mengidentifikasi mahasiswa berisiko tinggi, dengan hasil yang menunjukkan bahwa variabel akademik dan sosial ekonomi sangat berpengaruh terhadap risiko dropout. Sementara itu, Gray & Perkins (2019) menyoroti pentingnya data longitudinal dan variabel non-akademik dalam meningkatkan akurasi prediksi. Algoritma yang sering digunakan antara lain Random Forest, Logistic Regression, dan Support Vector Machine, dengan metrik evaluasi seperti akurasi, F1-score, dan ROC-AUC.
</p>
<ul>
  <li>Tamhane, A., et al. (2014). Predicting student risks through longitudinal analysis. <i>Proceedings of the 20th ACM SIGKDD international conference on Knowledge discovery and data mining</i>.</li>
  <li>Gray, G., & Perkins, D. (2019). Utilizing machine learning to predict student outcomes. <i>Journal of Educational Data Mining, 11(2), 1-17</i>.</li>
  <li>Education Data Initiative. (2023). College Dropout Rates.</li>
</ul>


<hr>

<h2>Business Understanding</h2>
<h3>Problem Statements</h3>
<ul>
  <li>Apa saja faktor utama yang berkontribusi terhadap dropout mahasiswa?</li>
  <li>Bagaimana cara mengidentifikasi mahasiswa yang paling berisiko keluar sebelum lulus?</li>
</ul>
<h3>Goals</h3>
<ul>
  <li>Mengidentifikasi variabel-variabel kunci yang memengaruhi risiko dropout mahasiswa.</li>
  <li>Mengembangkan model prediksi untuk mengklasifikasikan mahasiswa berdasarkan risiko dropout sehingga institusi dapat melakukan intervensi dini.</li>
</ul>
<h3>Solution Statement</h3>
<ul>
  <li>Menggunakan algoritma Random Forest dan Logistic Regression untuk membangun model prediksi status dropout.</li>
  <li>Melakukan hyperparameter tuning pada model Random Forest untuk meningkatkan performa prediksi.</li>
  <li>Memilih model terbaik berdasarkan metrik balanced accuracy, F1-score, dan ROC-AUC.</li>
</ul>

# Data Understanding
<p>
Dataset yang digunakan berasal dari Kaggle: <a href="https://www.kaggle.com/datasets/thedevastator/higher-education-predictors-of-student-retention/data" target="_blank">Higher Education Predictors of Student Retention</a>.
Dataset ini terdiri dari 4.424 data mahasiswa dengan 35 fitur. Berikut rincian variabel utama beserta tipe datanya setelah proses penyesuaian tipe data:
</p>
<table border="1" cellpadding="4" cellspacing="0">
  <tr>
    <th>Nama Variabel</th>
    <th>Tipe Data</th>
    <th>Deskripsi</th>
  </tr>
  <!-- Kategori (categorical) -->
  <tr><td>Marital status</td><td>Kategorikal (category)</td><td>Status pernikahan</td></tr>
  <tr><td>Application mode</td><td>Kategorikal (category)</td><td>Jalur pendaftaran</td></tr>
  <tr><td>Course</td><td>Kategorikal (category)</td><td>Kode program studi</td></tr>
  <tr><td>Daytime/evening attendance</td><td>Kategorikal (category)</td><td>Waktu kuliah (siang/malam)</td></tr>
  <tr><td>Previous qualification</td><td>Kategorikal (category)</td><td>Kualifikasi pendidikan terakhir</td></tr>
  <tr><td>Nacionality</td><td>Kategorikal (category)</td><td>Kewarganegaraan</td></tr>
  <tr><td>Mother's qualification</td><td>Kategorikal (category)</td><td>Kualifikasi ibu</td></tr>
  <tr><td>Father's qualification</td><td>Kategorikal (category)</td><td>Kualifikasi ayah</td></tr>
  <tr><td>Mother's occupation</td><td>Kategorikal (category)</td><td>Pekerjaan ibu</td></tr>
  <tr><td>Father's occupation</td><td>Kategorikal (category)</td><td>Pekerjaan ayah</td></tr>
  <tr><td>Gender</td><td>Kategorikal (category)</td><td>Jenis kelamin</td></tr>
  <tr><td>Scholarship holder</td><td>Kategorikal (category)</td><td>Status beasiswa</td></tr>
  <tr><td>Debtor</td><td>Kategorikal (category)</td><td>Status hutang</td></tr>
  <tr><td>Tuition fees up to date</td><td>Kategorikal (category)</td><td>Status pembayaran SPP</td></tr>
  <tr><td>Target</td><td>Kategorikal (category)</td><td>Status mahasiswa (Dropout, Graduate, Enrolled)</td></tr>

  <!-- Integer -->
  <tr><td>Application order</td><td>Numerik (int64)</td><td>Urutan pilihan program</td></tr>
  <tr><td>Age at enrollment</td><td>Numerik (int64)</td><td>Usia saat masuk</td></tr>
  <tr><td>Curricular units 1st sem (credited)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah semester 1 yang diakui</td></tr>
  <tr><td>Curricular units 1st sem (enrolled)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah diambil semester 1</td></tr>
  <tr><td>Curricular units 1st sem (evaluations)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah dievaluasi semester 1</td></tr>
  <tr><td>Curricular units 1st sem (approved)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah lulus semester 1</td></tr>
  <tr><td>Curricular units 1st sem (without evaluations)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah tanpa evaluasi semester 1</td></tr>
  <tr><td>Curricular units 2nd sem (credited)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah semester 2 yang diakui</td></tr>
  <tr><td>Curricular units 2nd sem (enrolled)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah diambil semester 2</td></tr>
  <tr><td>Curricular units 2nd sem (evaluations)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah dievaluasi semester 2</td></tr>
  <tr><td>Curricular units 2nd sem (approved)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah lulus semester 2</td></tr>
  <tr><td>Curricular units 2nd sem (without evaluations)</td><td>Numerik (int64)</td><td>Jumlah mata kuliah tanpa evaluasi semester 2</td></tr>

  <!-- Float -->
  <tr><td>Curricular units 1st sem (grade)</td><td>Numerik (float64)</td><td>Rata-rata nilai semester 1</td></tr>
  <tr><td>Curricular units 2nd sem (grade)</td><td>Numerik (float64)</td><td>Rata-rata nilai semester 2</td></tr>
  <tr><td>Unemployment rate</td><td>Numerik (float64)</td><td>Tingkat pengangguran nasional</td></tr>
  <tr><td>Inflation rate</td><td>Numerik (float64)</td><td>Tingkat inflasi nasional</td></tr>
  <tr><td>GDP</td><td>Numerik (float64)</td><td>Produk domestik bruto</td></tr>
</table>


<h3>Check data Duplikasi dan Missing Value</h3>
