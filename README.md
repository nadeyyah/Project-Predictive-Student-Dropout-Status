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

<h2>Hasil Exploratory Data Analysis (EDA)</h2>

<h3>Distribusi Status Mahasiswa</h3>
<img src="https://drive.google.com/uc?export=view&id=1CCRtfD4OnICRj1bYlL1qRkcMOcfndGoM" alt="Pie Chart Status Mahasiswa" width="350" />
<ul>
  <li><b>Dropout:</b> 49,9%</li>
  <li><b>Graduate:</b> 32,1%</li>
  <li><b>Enrolled:</b> 17,9%</li>
</ul>
<p><b>Insight:</b> Mayoritas mahasiswa dalam dataset berstatus dropout. Hal ini menunjukkan isu retensi mahasiswa sangat signifikan dan perlu perhatian khusus dalam pengembangan model prediksi.</p>

<h3>Statistik Deskriptif Fitur Numerik</h3>
<p>Berdasarkan statistik deskriptif, ditemukan bahwa:</p>
<ul>
  <li>Rata-rata usia mahasiswa saat masuk adalah 23,3 tahun (rentang 17–70 tahun).</li>
  <li>Rata-rata jumlah mata kuliah yang diambil semester 1: 6,27 (min: 0, max: 26).</li>
  <li>Rata-rata nilai semester 1: 10,64 (skala 0-20).</li>
</ul>
<p>Mayoritas mahasiswa berusia muda (18–25 tahun) dan mengambil 5-7 mata kuliah per semester.</p>
<img src="https://drive.google.com/uc?export=view&id=1BxLGRFT6VO-9yyy5UB5owwyhh55kd4Xo" alt="Histogram Fitur Numerik" width="700" />

<h3>Korelasi Antar Fitur Numerik</h3>
<img src="https://drive.google.com/uc?export=view&id=1BCVxNE4pi6yfjILhiMTuC_teNBKkoqD6" alt="Heatmap Korelasi" width="700" />
<ul>
  <li>Fitur akademik seperti jumlah mata kuliah lulus dan rata-rata nilai semester memiliki korelasi positif yang kuat satu sama lain.</li>
  <li>Faktor ekonomi makro (unemployment rate, inflation rate, GDP) tidak memiliki korelasi kuat dengan fitur akademik.</li>
</ul>
<p><b>Insight:</b> Faktor akademik lebih dominan dalam membedakan status mahasiswa dibanding faktor ekonomi makro.</p>

<h3>Analisis Outlier</h3>
<img src="https://drive.google.com/uc?export=view&id=1F--xI9AeFHx0u2-qwzfsRUItWEItKUFR" alt="Boxplot Outlier" width="700" />
<ul>
  <li>Outlier ditemukan pada fitur usia masuk, jumlah mata kuliah, dan nilai semester.</li>
  <li>Mahasiswa dengan nilai rendah dan jumlah mata kuliah lulus sedikit cenderung berisiko dropout.</li>
</ul>

<h3>Uji Chi-Square untuk Fitur Kategorikal</h3>
<p>Uji chi-square dilakukan untuk mengetahui ada tidaknya hubungan signifikan antara fitur kategorikal dan status mahasiswa (<i>Target</i>).</p>
<table border="1" cellpadding="4" cellspacing="0">
  <tr>
    <th>Variabel</th>
    <th>P-value</th>
    <th>Signifikan?</th>
  </tr>
  <tr><td>Marital status</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Application mode</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Course</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Daytime/evening attendance</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Previous qualification</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Mother's qualification</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Father's qualification</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Mother's occupation</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Father's occupation</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Gender</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Displaced</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Debtor</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Tuition fees up to date</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Scholarship holder</td><td>0.00000</td><td>Ya</td></tr>
  <tr><td>Nationality</td><td>0.24223</td><td>Tidak</td></tr>
  <tr><td>International</td><td>0.52731</td><td>Tidak</td></tr>
  <tr><td>Educational special needs</td><td>0.72540</td><td>Tidak</td></tr>
</table>
<p><b>Hipotesis Umum Uji Chi-Square:</b><br />
H0: Tidak ada hubungan antara variabel kategorikal dengan status mahasiswa (Target).<br />
H1: Ada hubungan antara variabel kategorikal dengan status mahasiswa (Target).<br />
<b>Hasil:</b> Sebagian besar fitur kategorikal memiliki hubungan signifikan dengan status mahasiswa (p-value &lt; 0,05), kecuali Nationality, International, dan Educational special needs.</p>

<h3>Kesimpulan EDA</h3>
<ul>
  <li>Status dropout mendominasi populasi mahasiswa dalam data.</li>
  <li>Faktor akademik (jumlah mata kuliah lulus, nilai semester) dan faktor finansial (debt, pembayaran SPP) sangat berpengaruh terhadap status mahasiswa.</li>
  <li>Beberapa fitur kategorikal seperti Nationality, International, dan Educational special needs tidak berpengaruh signifikan terhadap status mahasiswa.</li>
  <li>Outlier perlu diperhatikan dalam proses data preparation dan modeling.</li>
</ul>


# Data Preparation
<h2>Data Preparation</h2>

<p>
Pada tahap ini, data dipersiapkan untuk pemodelan dengan langkah-langkah sebagai berikut:
</p>
<ul>
  <li>
    <b>Penghapusan Kategori "Enrolled":</b>
    Data mahasiswa dengan status <i>Enrolled</i> dihapus dari dataset karena mereka masih aktif belajar dan belum memiliki outcome akhir. Model hanya akan memprediksi antara <i>Dropout</i> dan <i>Graduate</i>.
  </li>
  <li>
    <b>Menghapus Fitur yang Tidak Relevan:</b>
    Fitur-fitur yang tidak memberikan kontribusi signifikan terhadap prediksi atau bersifat redundan dihapus dari dataset. Contoh fitur yang di-drop dapat berupa ID, kode unik, atau fitur yang hasil analisis EDA/statistik menunjukkan tidak berpengaruh (misal: <i>Nationality</i>, <i>International</i>, <i>Educational special needs</i>).
  </li>
  <li>
    <b>Eliminasi Fitur Berdasarkan Korelasi:</b>
    Untuk mengurangi redundansi dan multikolinearitas, dilakukan eliminasi fitur dengan menggunakan threshold korelasi rendah dan tinggi:
    <ul>
      <li>Fitur dengan korelasi absolut di bawah 0.5 dipertimbangkan untuk dihapus jika kurang relevan.</li>
      <li>Fitur dengan korelasi absolut di atas 0.8 dihapus salah satunya untuk menghindari duplikasi informasi.</li>
    </ul>
  </li>
  <li>
    <b>Encoding Fitur Kategorikal:</b>
    Fitur kategorikal diubah menjadi numerik menggunakan <b>binary encoding</b>. Teknik ini efisien untuk fitur dengan banyak kategori dan mengurangi dimensi data.
  </li>
  <li>
    <b>Penanganan Outlier dengan IQR:</b>
    Outlier pada fitur numerik diidentifikasi dan dapat ditangani menggunakan metode Interquartile Range (IQR).
  </li>
  <li>
    <b>Transformasi Logaritmik:</b>
    Fitur numerik yang skewed (miring) ditransformasi menggunakan logaritma untuk mendekati distribusi normal.
  </li>
  <li>
    <b>Standarisasi Data:</b>
    Fitur numerik diskalakan menggunakan StandardScaler agar memiliki mean 0 dan standar deviasi 1.
  </li>
</ul>

<h3>Rumus dan Penjelasan Teknik yang Digunakan</h3>
<ul>
  <li><b>Interquartile Range (IQR):</b>
    <pre>
IQR = Q3 - Q1
Batas bawah = Q1 - 1.5 × IQR
Batas atas = Q3 + 1.5 × IQR
    </pre>
    Data di luar batas tersebut dianggap outlier.
  </li>
  <li><b>Transformasi Logaritmik:</b>
    <pre>
X_transformed = log(X + 1)
    </pre>
    Penambahan 1 untuk menghindari log(0).
  </li>
  <li><b>Standarisasi (StandardScaler):</b>
    <pre>
X_scaled = (X - μ) / σ
    </pre>
    μ adalah rata-rata fitur, σ adalah standar deviasi.
  </li>
</ul>

<h3>Eliminasi Fitur Berdasarkan Korelasi</h3>

<p>
Untuk meningkatkan kualitas data dan performa model, dilakukan eliminasi fitur berdasarkan analisis korelasi antar fitur numerik dengan menggunakan dua threshold:
</p>

<ul>
  <li><b>Threshold Korelasi Rendah (0.5):</b> Fitur dengan korelasi absolut di bawah 0.5 dianggap memiliki hubungan yang lemah dengan fitur lain dan dapat dipertimbangkan untuk dihapus jika kurang relevan.</li>
  <li><b>Threshold Korelasi Tinggi (0.8):</b> Fitur dengan korelasi absolut di atas 0.8 menunjukkan redundansi tinggi, sehingga salah satu fitur dari pasangan tersebut dihapus untuk mengurangi multikolinearitas dan kompleksitas model.</li>
</ul>

<p>
Langkah-langkah yang dilakukan:
</p>
<ol>
  <li>Menghitung matriks korelasi fitur numerik.</li>
  <li>Mengidentifikasi fitur dengan korelasi rendah (|r| &lt; 0.5) dan mempertimbangkan penghapusan berdasarkan relevansi domain.</li>
  <li>Mengidentifikasi fitur dengan korelasi tinggi (|r| &gt; 0.8) dan menghapus fitur yang kurang penting untuk mengurangi redundansi.</li>
  <li>Memastikan fitur yang tersisa memiliki korelasi moderat yang sehat agar informasi tetap terjaga.</li>
</ol>

<p>
Dengan eliminasi ini, dataset menjadi lebih ringkas, mengurangi risiko overfitting, dan memudahkan interpretasi model.
</p>

# Modeling

<p>
Pada tahap ini, data yang telah dipersiapkan digunakan untuk membangun dan mengevaluasi model machine learning.
</p>

<h3>Pembagian Data</h3>
<ul>
  <li>Dataset dibagi menjadi data latih (train) dan data uji (test) menggunakan <code>train_test_split</code> agar evaluasi model lebih objektif dan menghindari data leakage.</li>
</ul>

<h3>Pemilihan Model</h3>
<ul>
  <li>
    <b>Random Forest Classifier</b>
    <ul>
      <li>
        <b>Alasan pemilihan:</b>
        <ul>
          <li>Random Forest adalah model ensemble berbasis pohon keputusan yang sangat powerful untuk klasifikasi dengan banyak fitur, baik numerik maupun kategorikal.</li>
          <li>Mampu menangani data dengan missing value dan outlier lebih baik dibanding model linear.</li>
          <li>Memiliki mekanisme internal untuk mengukur feature importance sehingga membantu interpretasi hasil.</li>
          <li>Dengan class_weight='balanced', Random Forest dapat mengatasi masalah imbalance class pada target.</li>
        </ul>
      </li>
      <li>
        <b>Kelebihan:</b> Robust terhadap overfitting (dengan jumlah pohon yang cukup), dapat menangani data non-linear, dan memberikan hasil yang stabil.</li>
      <li>
        <b>Kekurangan:</b> Interpretasi model lebih sulit dibanding model linear, waktu komputasi lebih lama pada dataset besar.
      </li>
    </ul>
  </li>
  <li>
    <b>Logistic Regression</b>
    <ul>
      <li>
        <b>Alasan pemilihan:</b>
        <ul>
          <li>Model baseline yang sederhana dan mudah diinterpretasi.</li>
          <li>Cocok untuk klasifikasi biner dan memberikan probabilitas prediksi yang jelas.</li>
          <li>Memungkinkan analisis awal hubungan antara fitur dan target sebelum menggunakan model kompleks.</li>
        </ul>
      </li>
      <li>
        <b>Kelebihan:</b> Cepat, mudah diinterpretasi, dan efisien untuk data dengan hubungan linier.</li>
      <li>
        <b>Kekurangan:</b> Kurang efektif untuk data dengan hubungan non-linear kompleks dan sensitif terhadap outlier.
      </li>
    </ul>
  </li>
</ul>

<h3>Langkah-langkah Modeling</h3>
<ul>
  <li>Pembagian data menjadi train dan test.</li>
  <li>Pelatihan model Random Forest dan Logistic Regression pada data train.</li>
  <li>Hyperparameter tuning pada Random Forest menggunakan <code>GridSearchCV</code> atau <code>RandomizedSearchCV</code> untuk mencari parameter terbaik.</li>
  <li>Analisis feature importance pada Random Forest untuk mengetahui fitur paling berpengaruh.</li>
  <li>Evaluasi performa model pada data test menggunakan berbagai metrik.</li>
</ul>

<h3>Snippet Kode Pembagian Data dan Training (Contoh)</h3>
<pre>
from sklearn.model_selection import train_test_split

# X = fitur, y = target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Training Random Forest
from sklearn.ensemble import RandomForestClassifier
rf = RandomForestClassifier(class_weight='balanced', random_state=42)
rf.fit(X_train, y_train)

# Training Logistic Regression
from sklearn.linear_model import LogisticRegression
lr = LogisticRegression(class_weight='balanced', max_iter=1000, random_state=42)
lr.fit(X_train, y_train)
</pre>

<h2>Evaluation</h2>

<p>
Evaluasi model dilakukan untuk mengetahui seberapa baik model dalam mengklasifikasikan mahasiswa ke dalam kategori <b>Dropout</b> dan <b>Graduate</b>. Pada proyek ini, digunakan beberapa metrik evaluasi utama:
</p>

<ul>
  <li>
    <b>Balanced Accuracy</b>
    <ul>
      <li>
        <b>Rumus:</b><br>
        <pre>
Balanced Accuracy = (Recall_Kelas_1 + Recall_Kelas_2) / 2

dengan Recall = True Positives / (True Positives + False Negatives)
        </pre>
      </li>
      <li>
        <b>Alasan Penggunaan:</b> Balanced accuracy sangat penting ketika data tidak seimbang (jumlah dropout dan graduate berbeda jauh). Metrik ini menghitung rata-rata recall dari masing-masing kelas sehingga tidak bias terhadap kelas mayoritas.
      </li>
    </ul>
  </li>

  <li>
    <b>Recall (True Positive Rate)</b>
    <ul>
      <li>
        <b>Rumus:</b><br>
        <pre>
Recall = True Positives / (True Positives + False Negatives)
        </pre>
      </li>
      <li>
        <b>Penjelasan:</b> Recall mengukur kemampuan model untuk menemukan semua sampel positif yang sebenarnya. Ini sangat penting untuk mengetahui seberapa baik model dalam menangkap kelas positif (misal mahasiswa yang benar-benar dropout).
      </li>
    </ul>
  </li>

  <li>
    <b>F1 Score</b>
    <ul>
      <li>
        <b>Rumus:</b><br>
        <pre>
F1 = 2 × (Precision × Recall) / (Precision + Recall)

dengan Recall = True Positives / (True Positives + False Negatives)
        </pre>
      </li>
      <li>
        <b>Alasan Penggunaan:</b> F1 score digunakan karena menggabungkan precision dan recall dalam satu metrik. Sangat cocok untuk kasus data tidak seimbang, karena penalti terhadap false positive dan false negative.
      </li>
    </ul>
  </li>

  <li>
    <b>ROC-AUC (Receiver Operating Characteristic - Area Under Curve)</b>
    <ul>
      <li>
        <b>Rumus:</b><br>
        <pre>
ROC-AUC = Area di bawah kurva plot TPR (Recall) vs FPR (False Positive Rate)

dengan:
Recall (TPR) = True Positives / (True Positives + False Negatives)
FPR = False Positives / (False Positives + True Negatives)
        </pre>
      </li>
      <li>
        <b>Alasan Penggunaan:</b> ROC-AUC mengukur kemampuan model dalam membedakan antara dua kelas secara keseluruhan. Semakin tinggi nilai ROC-AUC (maksimum 1), semakin baik model dalam membedakan dropout dan graduate.
      </li>
    </ul>
  </li>

  <li>
    <b>Confusion Matrix</b>
    <ul>
      <li>
        <b>Rumus:</b><br>
        <pre>
|                | Prediksi Dropout | Prediksi Graduate |
|----------------|------------------|-------------------|
| Dropout        | True Negative    | False Positive    |
| Graduate       | False Negative   | True Positive     |
        </pre>
      </li>
      <li>
        <b>Alasan Penggunaan:</b> Confusion matrix memberikan gambaran detail distribusi prediksi benar dan salah, sehingga kita bisa mengetahui di mana model sering salah prediksi (misal: dropout diprediksi graduate).
      </li>
    </ul>
  </li>
</ul>


<h3>Hyperparameter Tuning</h3>
<p>
<b>Hyperparameter tuning</b> adalah proses mencari kombinasi parameter terbaik yang tidak dipelajari secara langsung oleh model dari data, tetapi sangat memengaruhi performa model. Contoh hyperparameter pada <b>Random Forest</b> antara lain jumlah pohon (<code>n_estimators</code>), kedalaman pohon (<code>max_depth</code>), dan jumlah fitur yang dipertimbangkan pada setiap split (<code>max_features</code>).
</p>

<ul>
  <li>
    <b>Alasan Melakukan Hyperparameter Tuning:</b>
    <ul>
      <li>Setiap model machine learning memiliki hyperparameter yang dapat diatur untuk mengoptimalkan kinerja model.</li>
      <li>Pengaturan default belum tentu memberikan hasil terbaik untuk dataset tertentu.</li>
      <li>Dengan tuning, model dapat mencapai performa maksimal dan menghindari overfitting atau underfitting.</li>
    </ul>
  </li>
  <li>
    <b>Cara Kerja:</b>
    <ul>
      <li>Proses tuning dilakukan dengan mencoba berbagai kombinasi nilai hyperparameter menggunakan metode seperti <b>Grid Search</b> atau <b>Randomized Search</b>.</li>
      <li>Setiap kombinasi diuji menggunakan cross-validation, dan dipilih kombinasi yang memberikan hasil evaluasi terbaik (misal: balanced accuracy tertinggi).</li>
    </ul>
  </li>
</ul>

<h3>Feature Importance</h3>

<p>
Setelah model dilatih, dilakukan analisis <b>feature importance</b> untuk mengetahui fitur-fitur apa saja yang paling berpengaruh dalam memprediksi status mahasiswa (<i>Dropout</i> atau <i>Graduate</i>).
</p>

<h3>1. Feature Importance pada Random Forest</h3>
<p>
Random Forest mengukur feature importance berdasarkan kontribusi setiap fitur dalam mengurangi impurity pada proses pemisahan node di seluruh pohon. Nilai importance yang lebih tinggi menunjukkan fitur tersebut lebih sering digunakan dan lebih berpengaruh dalam pengambilan keputusan model.
</p>

<h3>2. Feature Importance pada Logistic Regression</h3>
<p>
Pada Logistic Regression, "feature importance" diukur melalui nilai koefisien (weights) dari setiap fitur pada model. Koefisien positif menunjukkan fitur tersebut meningkatkan kemungkinan prediksi ke kelas target (misal: Dropout), sedangkan koefisien negatif menurunkan kemungkinan tersebut.
</p>

<h2>Hasil dan Pembahasan</h2>

<h3>Performa Model Awal (Binary Classification)</h3>
<ul>
  <li><b>Random Forest:</b>
    <ul>
      <li>Balanced Accuracy: 0.831</li>
      <li>F1 Score: 0.931</li>
      <li>AUC Score: 0.909</li>
    </ul>
  </li>
  <li><b>Logistic Regression:</b>
    <ul>
      <li>Balanced Accuracy: 0.835</li>
      <li>F1 Score: 0.902</li>
      <li>ROC AUC Score: 0.894</li>
    </ul>
  </li>
</ul>

<h3>Hasil Hyperparameter Tuning</h3>
<p>
Proses tuning dilakukan untuk meningkatkan performa model dengan mencari kombinasi parameter terbaik melalui cross-validation.<br>
Berikut parameter terbaik yang ditemukan:
</p>
<ul>
  <li><b>Random Forest:</b> {'max_depth': None, 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 200}</li>
  <li><b>Logistic Regression:</b> {'C': 10, 'penalty': 'l1', 'solver': 'liblinear'}</li>
</ul>

<h3>Evaluasi Model Setelah Hyperparameter Tuning</h3>
<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Model</th>
      <th>F1 Score</th>
      <th>AUC Score</th>
      <th>Balanced Accuracy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Random Forest</td>
      <td>0.928</td>
      <td>0.913</td>
      <td>0.829</td>
    </tr>
    <tr>
      <td>Logistic Regression</td>
      <td>0.902</td>
      <td>0.895</td>
      <td>0.835</td>
    </tr>
  </tbody>
</table>

<h3>Analisis Feature Importance</h3>

<h4>Random Forest</h4>
<table border="1" cellpadding="4" cellspacing="0">
  <thead>
    <tr>
      <th>Feature</th>
      <th>Importance</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Curricular units 2nd sem (approved)</td><td>0.240</td></tr>
    <tr><td>Curricular units 2nd sem (grade)</td><td>0.137</td></tr>
    <tr><td>Curricular units 2nd sem (evaluations)</td><td>0.089</td></tr>
    <tr><td>Curricular units 1st sem (evaluations)</td><td>0.081</td></tr>
    <tr><td>Course</td><td>0.067</td></tr>
    <tr><td>Tuition fees up to date</td><td>0.053</td></tr>
    <tr><td>Father's occupation</td><td>0.049</td></tr>
    <tr><td>Mother's occupation</td><td>0.043</td></tr>
    <tr><td>Application mode</td><td>0.040</td></tr>
    <tr><td>Mother's qualification</td><td>0.038</td></tr>
  </tbody>
</table>

<h4>Logistic Regression</h4>
<table border="1" cellpadding="4" cellspacing="0">
  <thead>
    <tr>
      <th>Feature</th>
      <th>Importance (Coefficient)</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Tuition fees up to date</td><td>2.533</td></tr>
    <tr><td>Curricular units 2nd sem (approved)</td><td>2.219</td></tr>
    <tr><td>Debtor</td><td>1.377</td></tr>
    <tr><td>Gender</td><td>0.772</td></tr>
    <tr><td>Displaced</td><td>0.639</td></tr>
    <tr><td>Scholarship holder</td><td>0.591</td></tr>
    <tr><td>Curricular units 1st sem (evaluations)</td><td>0.375</td></tr>
    <tr><td>Curricular units 2nd sem (grade)</td><td>0.201</td></tr>
    <tr><td>Curricular units 2nd sem (evaluations)</td><td>0.169</td></tr>
    <tr><td>Curricular units 2nd sem (enrolled)</td><td>0.125</td></tr>
  </tbody>
</table>

<h3>Perbandingan Model dengan 10 Fitur Teratas</h3>
<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Model</th>
      <th>F1 Score</th>
      <th>AUC Score</th>
      <th>Balanced Accuracy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Random Forest (Top 10 Features)</td>
      <td>0.932</td>
      <td>0.893</td>
      <td>0.841</td>
    </tr>
    <tr>
      <td>Logistic Regression (Top 10 Features)</td>
      <td>0.895</td>
      <td>0.875</td>
      <td>0.833</td>
    </tr>
  </tbody>
</table>

<h3>Pembahasan</h3>
<p>
Hasil evaluasi menunjukkan bahwa kedua model, Random Forest dan Logistic Regression, memiliki performa yang baik dalam memprediksi status mahasiswa antara dropout dan graduate. Random Forest sedikit unggul dalam F1 Score dan Balanced Accuracy setelah hyperparameter tuning, menunjukkan kemampuannya menangani data yang kompleks dan non-linear.
</p>
<p>
Logistic Regression, meskipun model yang lebih sederhana, tetap memberikan hasil yang kompetitif dan memberikan interpretasi yang mudah melalui koefisien fitur. Hal ini penting untuk memahami pengaruh masing-masing fitur secara langsung terhadap risiko dropout.
</p>
<p>
Analisis feature importance mengungkapkan bahwa fitur akademik seperti jumlah mata kuliah yang disetujui dan nilai semester 2, serta faktor finansial seperti status pembayaran SPP dan status hutang, merupakan faktor utama yang mempengaruhi risiko dropout. Hal ini konsisten dengan literatur dan menunjukkan bahwa intervensi yang fokus pada peningkatan performa akademik dan dukungan finansial dapat membantu menurunkan angka dropout.
</p>
<p>
Penggunaan hyperparameter tuning berhasil meningkatkan performa model, terutama pada Random Forest, dengan parameter optimal yang ditemukan adalah <code>n_estimators=200</code>, <code>max_depth=None</code>, <code>min_samples_leaf=1</code>, dan <code>min_samples_split=2</code>. Sedangkan Logistic Regression terbaik menggunakan regularisasi L1 dengan <code>C=10</code>.
</p>
<p>
Secara keseluruhan, model Random Forest dengan tambahan top 10 Importance Feature dipilih sebagai model akhir karena performa yang lebih baik dan kemampuan menangani kompleksitas data, sementara Logistic Regression tetap berguna sebagai baseline dan untuk interpretasi.
</p>
<h3>Ringkasan Klasifikasi Risiko (Risk Classification Summary)</h3>

<p>
Berdasarkan hasil prediksi model, mahasiswa diklasifikasikan ke dalam dua kategori risiko utama terkait dropout:
</p>
<ul>
  <li><b>High Risk:</b> 1.493 mahasiswa</li>
  <li><b>Moderate Risk:</b> 192 mahasiswa</li>
</ul>

<p>
Tabel berikut menunjukkan contoh data mahasiswa pada masing-masing kategori risiko beserta beberapa fitur penting yang berkontribusi terhadap klasifikasi tersebut:
</p>

<table border="1" cellpadding="4" cellspacing="0">
  <thead>
    <tr>
      <th>Curricular units 2nd sem (approved)</th>
      <th>Curricular units 2nd sem (grade)</th>
      <th>Curricular units 2nd sem (evaluations)</th>
      <th>Curricular units 1st sem (evaluations)</th>
      <th>Course</th>
      <th>Tuition fees up to date</th>
      <th>Father's occupation</th>
      <th>Mother's occupation</th>
      <th>Application mode</th>
      <th>Mother's qualification</th>
      <th>Overall Risk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>10.68</td>
      <td>20.88</td>
      <td>1.54</td>
      <td>1.82</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>High Risk</td>
    </tr>
    <tr>
      <td>5.28</td>
      <td>11.26</td>
      <td>8.28</td>
      <td>4.64</td>
      <td>13.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>16.0</td>
      <td>Moderate Risk</td>
    </tr>
    <tr>
      <td>10.68</td>
      <td>15.25</td>
      <td>1.54</td>
      <td>6.53</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>15.0</td>
      <td>High Risk</td>
    </tr>
    <tr>
      <td>10.68</td>
      <td>25.83</td>
      <td>2.76</td>
      <td>4.64</td>
      <td>8.0</td>
      <td>1.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>High Risk</td>
    </tr>
  </tbody>
</table>

<p>
Model prediksi berhasil mengidentifikasi mahasiswa yang berisiko tinggi dan sedang terkait dropout berdasarkan fitur-fitur akademik dan finansial utama. Mahasiswa dengan risiko tinggi umumnya memiliki:
</p>
<ul>
  <li>Jumlah mata kuliah yang disetujui pada semester 2 yang rendah atau nilai semester 2 yang kurang memuaskan.</li>
  <li>Jumlah evaluasi semester 1 dan 2 yang relatif sedikit, menunjukkan keterlibatan akademik yang rendah.</li>
  <li>Status pembayaran SPP yang tidak lancar (nilai rendah pada fitur <i>Tuition fees up to date</i>).</li>
  <li>Faktor sosial ekonomi seperti pekerjaan orang tua dan jalur pendaftaran yang juga berkontribusi pada risiko.</li>
</ul>

<p>
Mahasiswa dengan risiko sedang cenderung memiliki performa akademik dan kondisi finansial yang lebih baik dibandingkan kelompok risiko tinggi, tetapi masih membutuhkan perhatian agar tidak beralih ke risiko tinggi.
</p>

<p>
Dengan klasifikasi risiko ini, institusi dapat melakukan intervensi yang lebih terfokus, seperti memberikan dukungan akademik dan finansial kepada mahasiswa berisiko tinggi untuk meningkatkan retensi dan keberhasilan studi.
</p>
****
