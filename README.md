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
Dataset ini terdiri dari 4.424 data mahasiswa dengan 35 fitur. Berikut rincian variabel utama beserta tipe datanya:
<table border="1" cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr style="background-color: #f2f2f2;">
      <th style="text-align: left;">Nama Variabel</th>
      <th style="text-align: left;">Tipe Data</th>
      <th style="text-align: left;">Deskripsi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Marital status</td>
      <td>Numerik (int64)</td>
      <td>Status pernikahan mahasiswa saat masuk (misalnya: belum menikah, menikah), dikodekan dalam bentuk angka.</td>
    </tr>
    <tr>
      <td>Application mode</td>
      <td>Numerik (int64)</td>
      <td>Jalur atau metode pendaftaran mahasiswa ke perguruan tinggi (misalnya: reguler, transfer), dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Application order</td>
      <td>Numerik (int64)</td>
      <td>Urutan pilihan program studi yang diajukan oleh mahasiswa saat mendaftar.</td>
    </tr>
    <tr>
      <td>Course</td>
      <td>Numerik (int64)</td>
      <td>Kode program studi atau jurusan yang dipilih oleh mahasiswa.</td>
    </tr>
    <tr>
      <td>Daytime/evening attendance</td>
      <td>Numerik (int64)</td>
      <td>Waktu kuliah yang diikuti mahasiswa, apakah kuliah siang atau malam, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Previous qualification</td>
      <td>Numerik (int64)</td>
      <td>Kualifikasi pendidikan terakhir yang dimiliki mahasiswa sebelum masuk perguruan tinggi, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Nacionality</td>
      <td>Numerik (int64)</td>
      <td>Kewarganegaraan mahasiswa, dikodekan dalam bentuk angka.</td>
    </tr>
    <tr>
      <td>Mother's qualification</td>
      <td>Numerik (int64)</td>
      <td>Kualifikasi pendidikan tertinggi ibu mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Father's qualification</td>
      <td>Numerik (int64)</td>
      <td>Kualifikasi pendidikan tertinggi ayah mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Mother's occupation</td>
      <td>Numerik (int64)</td>
      <td>Pekerjaan ibu mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Father's occupation</td>
      <td>Numerik (int64)</td>
      <td>Pekerjaan ayah mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Displaced</td>
      <td>Numerik (int64)</td>
      <td>Status mahasiswa apakah termasuk pengungsi atau pindahan, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Educational special needs</td>
      <td>Numerik (int64)</td>
      <td>Apakah mahasiswa memiliki kebutuhan pendidikan khusus, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Debtor</td>
      <td>Numerik (int64)</td>
      <td>Status hutang mahasiswa, apakah memiliki tunggakan atau tidak, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Tuition fees up to date</td>
      <td>Numerik (int64)</td>
      <td>Status pembayaran biaya kuliah mahasiswa, apakah sudah lunas atau belum, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Gender</td>
      <td>Numerik (int64)</td>
      <td>Jenis kelamin mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Scholarship holder</td>
      <td>Numerik (int64)</td>
      <td>Status penerima beasiswa mahasiswa, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Age at enrollment</td>
      <td>Numerik (int64)</td>
      <td>Usia mahasiswa saat mendaftar atau masuk perguruan tinggi.</td>
    </tr>
    <tr>
      <td>International</td>
      <td>Numerik (int64)</td>
      <td>Status mahasiswa apakah mahasiswa internasional atau bukan, dikodekan dalam angka.</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (credited)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 1 yang diakui (diberi kredit).</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (enrolled)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah yang diambil mahasiswa pada semester 1.</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (evaluations)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 1 yang dievaluasi (diberi nilai).</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (approved)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 1 yang lulus.</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (grade)</td>
      <td>Numerik (float64)</td>
      <td>Rata-rata nilai mata kuliah semester 1.</td>
    </tr>
    <tr>
      <td>Curricular units 1st sem (without evaluations)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 1 tanpa evaluasi atau penilaian.</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (credited)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 2 yang diakui (diberi kredit).</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (enrolled)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah yang diambil mahasiswa pada semester 2.</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (evaluations)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 2 yang dievaluasi.</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (approved)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 2 yang lulus.</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (grade)</td>
      <td>Numerik (float64)</td>
      <td>Rata-rata nilai mata kuliah semester 2.</td>
    </tr>
    <tr>
      <td>Curricular units 2nd sem (without evaluations)</td>
      <td>Numerik (int64)</td>
      <td>Jumlah mata kuliah semester 2 tanpa evaluasi.</td>
    </tr>
    <tr>
      <td>Unemployment rate</td>
      <td>Numerik (float64)</td>
      <td>Tingkat pengangguran nasional pada saat mahasiswa mendaftar.</td>
    </tr>
    <tr>
      <td>Inflation rate</td>
      <td>Numerik (float64)</td>
      <td>Tingkat inflasi nasional pada saat mahasiswa mendaftar.</td>
    </tr>
    <tr>
      <td>GDP</td>
      <td>Numerik (float64)</td>
      <td>Produk domestik bruto nasional pada saat mahasiswa mendaftar.</td>
    </tr>
    <tr>
      <td>Target</td>
      <td>Kategorikal (object)</td>
      <td>Status akhir mahasiswa: Dropout (berhenti kuliah), Graduate (lulus), atau Enrolled (masih aktif).</td>
    </tr>
  </tbody>
</table>

dari tabel di atas, ada beberapa variabel yang perlu dilakukan penyesuaian terkait tipe data dan terdapat pula nama variabel dengan penulisan yang salah. Berikut hasil dari perbaikan tipe data dan perbaikan nama variabel <b> Nacionality </b> menjadi <b> Nationality </b>

<body>
  <pre>
&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 4424 entries, 0 to 4423
Data columns (total 35 columns):
 #   Column                                          Non-Null Count  Dtype   
---  ------                                          --------------  -----   
 0   Marital status                                  4424 non-null   category
 1   Application mode                                4424 non-null   category
 2   Application order                               4424 non-null   int64   
 3   Course                                          4424 non-null   category
 4   Daytime/evening attendance                      4424 non-null   category
 5   Previous qualification                          4424 non-null   category
 6   Nationality                                     4424 non-null   category
 7   Mother's qualification                          4424 non-null   category
 8   Father's qualification                          4424 non-null   category
 9   Mother's occupation                             4424 non-null   category
 10  Father's occupation                             4424 non-null   category
 11  Displaced                                       4424 non-null   category
 12  Educational special needs                       4424 non-null   category
 13  Debtor                                          4424 non-null   category
 14  Tuition fees up to date                         4424 non-null   category
 15  Gender                                          4424 non-null   category
 16  Scholarship holder                              4424 non-null   category
 17  Age at enrollment                               4424 non-null   int64   
 18  International                                   4424 non-null   category
 19  Curricular units 1st sem (credited)             4424 non-null   int64   
 20  Curricular units 1st sem (enrolled)             4424 non-null   int64   
 21  Curricular units 1st sem (evaluations)          4424 non-null   int64   
 22  Curricular units 1st sem (approved)             4424 non-null   int64   
 23  Curricular units 1st sem (grade)                4424 non-null   float64 
 24  Curricular units 1st sem (without evaluations)  4424 non-null   int64   
 25  Curricular units 2nd sem (credited)             4424 non-null   int64   
 26  Curricular units 2nd sem (enrolled)             4424 non-null   int64   
 27  Curricular units 2nd sem (evaluations)          4424 non-null   int64   
 28  Curricular units 2nd sem (approved)             4424 non-null   int64   
 29  Curricular units 2nd sem (grade)                4424 non-null   float64 
 30  Curricular units 2nd sem (without evaluations)  4424 non-null   int64   
 31  Unemployment rate                               4424 non-null   float64 
 32  Inflation rate                                  4424 non-null   float64 
 33  GDP                                             4424 non-null   float64 
 34  Target                                          4424 non-null   category
dtypes: category(18), float64(5), int64(12)
memory usage: 674.8 KB
  </pre>
</body>
</html>

<h3>Check Duplikasi data dan Missing Value</h3> 
Setelah dilakukan perbaikan tipe data dari variabel yang sesuai, dilakukan penge<i>chek</i>-an data yang duplikat serta data yang hilang. 
Tidak ditemukan data terduplikat dan missing value. 
<section>
  <pre><code># Checking Duplicate and Missing Value
print(df.duplicated().sum())
print(df.isnull().sum().sum())</code></pre>
  <h3>Output:</h3>
  <pre><code>0
0</code></pre>
</section>

<h3>Exploratory Data Analysis (EDA)</h3>

<section>
  <h3>1. Statistika Deskriptif</h3>
  <p>
    Statistik deskriptif memberikan gambaran umum tentang karakteristik variabel numerik dalam dataset. Dari hasil analisis, rata-rata usia mahasiswa saat masuk adalah sekitar 23 tahun dengan rentang usia 17 hingga 70 tahun. Jumlah mata kuliah yang diambil pada semester pertama dan kedua bervariasi, dengan rata-rata sekitar 6 mata kuliah per semester. Tingkat pengangguran nasional rata-rata sebesar 11,57% dan inflasi sekitar 1,23%. Variasi data terlihat dari standar deviasi yang cukup besar, menunjukkan keberagaman dalam data mahasiswa.
  </p>
<section>
  <table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; text-align: right;">
    <thead style="background-color: #f2f2f2;">
      <tr>
        <th style="text-align:left;">Variabel</th>
        <th>Count</th>
        <th>Mean</th>
        <th>Std</th>
        <th>Min</th>
        <th>25%</th>
        <th>50%</th>
        <th>75%</th>
        <th>Max</th>
      </tr>
    </thead>
    <tbody>
      <tr><td style="text-align:left;">Application order</td><td>4424</td><td>1.73</td><td>1.31</td><td>0</td><td>1</td><td>1</td><td>2</td><td>9</td></tr>
      <tr><td style="text-align:left;">Age at enrollment</td><td>4424</td><td>23.27</td><td>7.59</td><td>17</td><td>19</td><td>20</td><td>25</td><td>70</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (credited)</td><td>4424</td><td>0.71</td><td>2.36</td><td>0</td><td>0</td><td>0</td><td>0</td><td>20</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (enrolled)</td><td>4424</td><td>6.27</td><td>2.48</td><td>0</td><td>5</td><td>6</td><td>7</td><td>26</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (evaluations)</td><td>4424</td><td>8.30</td><td>4.18</td><td>0</td><td>6</td><td>8</td><td>10</td><td>45</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (approved)</td><td>4424</td><td>4.71</td><td>3.09</td><td>0</td><td>3</td><td>5</td><td>6</td><td>26</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (grade)</td><td>4424</td><td>10.64</td><td>4.84</td><td>0</td><td>11</td><td>12.29</td><td>13.40</td><td>18.88</td></tr>
      <tr><td style="text-align:left;">Curricular units 1st sem (without evaluations)</td><td>4424</td><td>0.14</td><td>0.69</td><td>0</td><td>0</td><td>0</td><td>0</td><td>12</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (credited)</td><td>4424</td><td>0.54</td><td>1.92</td><td>0</td><td>0</td><td>0</td><td>0</td><td>19</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (enrolled)</td><td>4424</td><td>6.23</td><td>2.20</td><td>0</td><td>5</td><td>6</td><td>7</td><td>23</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (evaluations)</td><td>4424</td><td>8.06</td><td>3.95</td><td>0</td><td>6</td><td>8</td><td>10</td><td>33</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (approved)</td><td>4424</td><td>4.44</td><td>3.01</td><td>0</td><td>2</td><td>5</td><td>6</td><td>20</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (grade)</td><td>4424</td><td>10.23</td><td>5.21</td><td>0</td><td>10.75</td><td>12.20</td><td>13.33</td><td>18.57</td></tr>
      <tr><td style="text-align:left;">Curricular units 2nd sem (without evaluations)</td><td>4424</td><td>0.15</td><td>0.75</td><td>0</td><td>0</td><td>0</td><td>0</td><td>12</td></tr>
      <tr><td style="text-align:left;">Unemployment rate</td><td>4424</td><td>11.57</td><td>2.66</td><td>7.60</td><td>9.40</td><td>11.10</td><td>13.90</td><td>16.20</td></tr>
      <tr><td style="text-align:left;">Inflation rate</td><td>4424</td><td>1.23</td><td>1.38</td><td>-0.80</td><td>0.30</td><td>1.40</td><td>2.60</td><td>3.70</td></tr>
      <tr><td style="text-align:left;">GDP</td><td>4424</td><td>0.00</td><td>2.27</td><td>-4.06</td><td>-1.70</td><td>0.32</td><td>1.79</td><td>3.51</td></tr>
    </tbody>
  </table>
</section>


  <h3>2. Sebaran Status Mahasiswa</h3>
  <p>
    Diagram pie chart menunjukkan distribusi status mahasiswa (Dropout, Graduate, Enrolled). Visualisasi ini mengungkapkan bahwa proporsi mahasiswa yang dropout cukup tinggi, yang menjadi perhatian penting dalam analisis keberhasilan studi.
  </p>
  <img src= "https://raw.githubusercontent.com/nadeyyah/Project-Predictive-Student-Dropout-Status/main/asset/asset_1.png" alt="Pie Chart Sebaran Status Mahasiswa" width="400" />
  <p><em>Sumber: <a href="https://github.com/nadeyyah/Project-Predictive-Student-Dropout-Status/blob/main/asset/asset_1.png">Diagram Pie chart </a></em></p>

  <h3>3. Hasil Pengujian Independesi Variabel Kategorik dengan Chi-square</h3>
  <p>
    Pengujian Chi-square digunakan untuk menguji hubungan antara variabel kategorik dengan status mahasiswa. Hipotesis yang diuji adalah:<br>
    <strong>H0:</strong> Tidak ada hubungan signifikan antara variabel kategorik dengan status mahasiswa.<br>
    <strong>H1:</strong> Ada hubungan signifikan antara variabel kategorik dengan status mahasiswa.<br>
    Berdasarkan hasil, sebagian besar variabel kategorik memiliki p-value &lt; 0.05, sehingga menolak H0 dan menyatakan ada hubungan signifikan. Variabel seperti Nationality, International, dan Educational special needs memiliki p-value besar, sehingga tidak menunjukkan hubungan signifikan.
  </p>
  <table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; margin-bottom: 1em;">
    <thead style="background-color: #f2f2f2;">
      <tr>
        <th>Variabel</th>
        <th>P-value</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Marital status</td><td>0.00000</td></tr>
      <tr><td>Application mode</td><td>0.00000</td></tr>
      <tr><td>Course</td><td>0.00000</td></tr>
      <tr><td>Daytime/evening attendance</td><td>0.00000</td></tr>
      <tr><td>Previous qualification</td><td>0.00000</td></tr>
      <tr><td>Mother's qualification</td><td>0.00000</td></tr>
      <tr><td>Father's qualification</td><td>0.00000</td></tr>
      <tr><td>Mother's occupation</td><td>0.00000</td></tr>
      <tr><td>Father's occupation</td><td>0.00000</td></tr>
      <tr><td>Displaced</td><td>0.00000</td></tr>
      <tr><td>Debtor</td><td>0.00000</td></tr>
      <tr><td>Tuition fees up to date</td><td>0.00000</td></tr>
      <tr><td>Gender</td><td>0.00000</td></tr>
      <tr><td>Scholarship holder</td><td>0.00000</td></tr>
      <tr><td>Target_encoded</td><td>0.00000</td></tr>
      <tr><td>Nationality</td><td>0.24223</td></tr>
      <tr><td>International</td><td>0.52731</td></tr>
      <tr><td>Educational special needs</td><td>0.72540</td></tr>
    </tbody>
  </table>

  <h3>4. Korelasi Pearson Variabel Numerik</h3>
  <p>
    Heatmap korelasi Pearson memperlihatkan hubungan antar variabel numerik. Korelasi positif yang kuat (ditandai warna merah) menunjukkan variabel yang saling berhubungan, misalnya antara jumlah mata kuliah yang diambil dan nilai rata-rata. Korelasi negatif atau lemah (warna biru) menunjukkan variabel yang kurang berhubungan. Informasi ini berguna untuk memahami pola dan hubungan dalam data numerik. itur akademik seperti jumlah mata kuliah lulus dan rata-rata nilai semester memiliki korelasi positif yang kuat satu sama lain.Faktor ekonomi makro (unemployment rate, inflation rate, GDP) tidak memiliki korelasi kuat dengan fitur akademik
  </p>
  <img src= "https://raw.githubusercontent.com/nadeyyah/Project-Predictive-Student-Dropout-Status/main/asset/asset_2.png" alt="Heatmap Korelasi Pearson" width="700" />
  <p><em>Sumber: <a href="https://github.com/nadeyyah/Project-Predictive-Student-Dropout-Status/blob/main/asset/asset_2.png">Heatmap Korelasi Pearson</a></em></p>

  <h3>5. Histogram Variabel Numerik</h3>
  <p>
    Histogram menampilkan distribusi frekuensi nilai pada variabel numerik. Sebagian besar variabel menunjukkan distribusi yang tidak simetris (skewed), yang mengindikasikan adanya variasi dan potensi outlier dalam data. Misalnya, usia mahasiswa memiliki distribusi yang cenderung normal dengan sedikit skewness.
  </p>
  <img src= "https://raw.githubusercontent.com/nadeyyah/Project-Predictive-Student-Dropout-Status/main/asset/asset_3.png" alt="Histogram Variabel Numerik" width="900" />
    <p><em>Sumber: <a href="https://github.com/nadeyyah/Project-Predictive-Student-Dropout-Status/blob/main/asset/asset_3.png">Histogram Variabel Numerik</a></em></p>

  <h3>6. Boxplot Variabel Numerik </h3>
  <p>
    Boxplot memberikan gambaran persebaran data, median, dan outlier pada setiap variabel numerik. Visualisasi ini membantu mengidentifikasi nilai ekstrim dan variasi antar mahasiswa, yang penting untuk analisis kualitas data dan deteksi anomali.Outlier ditemukan pada fitur usia masuk, jumlah mata kuliah, dan nilai semester. Mahasiswa dengan nilai rendah dan jumlah mata kuliah lulus sedikit cenderung berisiko dropout.
  </p>
  <img src= "https://raw.githubusercontent.com/nadeyyah/Project-Predictive-Student-Dropout-Status/main/asset/asset_4.png" alt="Boxplot Variabel Numerik" width="900" />
  <p><em>Sumber: <a href="https://github.com/nadeyyah/Project-Predictive-Student-Dropout-Status/blob/main/asset/asset_4.png">Boxplot Variabel Numerik</a></em></p>

  <h3>7. Chart Variabel Kategorik</h3>
  <p>
    Grafik batang menunjukkan proporsi status mahasiswa (Dropout, Graduate, Enrolled) pada setiap kategori variabel kategorik. Variabel seperti Marital status, Application mode, dan Debtor menunjukkan perbedaan proporsi status mahasiswa yang signifikan antar kategori, misalnya kategori dengan status hutang tinggi memiliki proporsi Dropout yang lebih besar. Variabel lain seperti Educational special needs dan International menunjukkan proporsi yang lebih seragam antar kategori.
  </p>
  <p>
    Visualisasi ini mendukung hasil uji chi-square dan membantu mengidentifikasi kategori risiko tinggi Dropout, sehingga dapat menjadi fokus intervensi untuk meningkatkan keberhasilan studi mahasiswa.
  </p>
  <img src= "https://raw.githubusercontent.com/nadeyyah/Project-Predictive-Student-Dropout-Status/main/asset/asset_6.png" alt="Chart Variabel Kategorik" width="900" />
  <p><em>Sumber: <a href="https://github.com/nadeyyah/Project-Predictive-Student-Dropout-Status/blob/main/asset/asset_6.png">Chart Variabel Kategorik</a></em></p>
</section>

# DATA PREPARATION
<section>
  <h3>1. Menghapus Fitur Kategorik yang Tidak Digunakan</h3>
  <p>
    Pada tahap awal, kolom-kolom kategorik yang tidak berpengaruh signifikan terhadap variabel target dihapus. Kolom <code>'Nationality'</code>, <code>'International'</code>, dan <code>'Educational special needs'</code> dihapus berdasarkan hasil uji statistik yang menunjukkan ketidaksignifikanannya.
  </p>

  <h3>2. Menghapus Fitur Numerik Berdasarkan Threshold Korelasi</h3>
  <p>
    Fitur numerik dievaluasi untuk multikolinearitas menggunakan threshold korelasi 0.8 (korelasi tinggi) dan 0.5 (korelasi maksimum rendah). Fitur dengan korelasi tinggi dihapus untuk mengurangi redundansi, sedangkan fitur dengan korelasi maksimum rendah juga dihapus karena kurang relevan. Hasilnya adalah:
  </p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Dropped columns due to high correlation: {'Curricular units 1st sem (credited)', 'Curricular units 1st sem (enrolled)', 'Curricular units 1st sem (approved)', 'Curricular units 1st sem (grade)'}
Dropped columns due to low max correlation with others: {'Unemployment rate', 'Application order', 'GDP', 'Inflation rate', 'Age at enrollment'}
Total dropped columns: {'Curricular units 1st sem (credited)', 'Curricular units 1st sem (approved)', 'Unemployment rate', 'Curricular units 1st sem (enrolled)', 'Application order', 'GDP', 'Inflation rate', 'Age at enrollment', 'Curricular units 1st sem (grade)'}
Shape of dataframe after dropping: (4424, 23)
  </pre>

  <h3>3. Penanganan Outlier </h3>
  <p>
    Outlier diidentifikasi dan dihapus menggunakan metode Interquartile Range (IQR). Rumus IQR adalah:
  </p>
  <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-size:1.05em; font-family: 'Consolas', 'Monaco', monospace;">
IQR = Q3 - Q1
  </pre>
  <p>
    Data yang berada di luar rentang 
  </p>
  <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-size:1.05em; font-family: 'Consolas', 'Monaco', monospace;">
[Q1 - 1.5 × IQR, Q3 + 1.5 × IQR]
  </pre>
  <p>dianggap outlier dan dihapus untuk meningkatkan kualitas data.</p>

  <h3>4. Transformasi Data Numerik dengan Log Transformation</h3>
  <p>
    Untuk mengurangi skewness dan menormalkan distribusi variabel numerik, dilakukan transformasi log menggunakan rumus:
  </p>
  <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-size:1.05em; font-family: 'Consolas', 'Monaco', monospace;">
X' = log(X + 1)
  </pre>
  <p>Berikut adalah nilai skewness setelah transformasi log:</p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Curricular units 1st sem (evaluations): 0.07
Curricular units 1st sem (without evaluations): 0.00
Curricular units 2nd sem (credited): 0.00
Curricular units 2nd sem (enrolled): -0.33
Curricular units 2nd sem (evaluations): 0.38
Curricular units 2nd sem (approved): -1.98
Curricular units 2nd sem (grade): 0.11
Curricular units 2nd sem (without evaluations): 0.00
  </pre>

  <h3>5. Skala Data Numerik dengan Standard Scaler</h3>
  <p>
    Data numerik diskalakan agar memiliki mean nol dan standar deviasi satu menggunakan Standard Scaler dengan rumus:
  </p>
  <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-size:1.05em; font-family: 'Consolas', 'Monaco', monospace;">
X scaled = (X - μ) / σ
  </pre>
  <p>di mana <em>μ</em> adalah rata-rata dan <em>σ</em> adalah standar deviasi dari fitur tersebut.</p>

  <h3>6. Encoding Fitur Kategorik dengan Ordinal Encoder</h3>
  <p>
    Fitur kategorik diencoding menggunakan Ordinal Encoder untuk mengubah kategori menjadi nilai integer. Metode ini dipilih karena beberapa fitur kategorik memiliki urutan atau tingkatan yang inheren, sehingga ordinal encoding dapat mempertahankan informasi urutan tersebut yang berguna untuk beberapa model.
  </p>

  <h3>7. Menghapus Kategori Target 'Enrolled'</h3>
  <p>
    Kategori target dengan label 1 (Enrolled) dihapus agar fokus analisis hanya pada mahasiswa yang lulus dan yang dropout. Setelah penghapusan, ukuran dataset menjadi:
  </p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">(1685, 23)</pre>

  <h3>8. Identifikasi Fitur untuk Klasifikasi</h3>
  <p>
    Variabel fitur <code>X</code> merupakan gabungan dari variabel numerik dan kategorik yang telah dipilih dan diproses, siap digunakan untuk pemodelan klasifikasi sedangkan <code> y </code> adalah Target .
  </p>

  <h3>9. Pembagian Data Training dan Testing</h3>
  <p>
    Data dibagi menjadi subset training dan testing dengan rasio 80:20. Selain itu, kelas dropout yang sebelumnya diberi label 2 diubah menjadi label 1 agar jarak kelas tidak terlalu berjauhan, memudahkan proses klasifikasi. Hasil pembagian data adalah sebagai berikut:
  </p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
X_train shape: (1348, 22)
X_test shape: (337, 22)

Distribusi y_train:
Target_encoded
1.0    0.746291
0.0    0.253709
Name: proportion, dtype: float64

Distribusi y_test:
Target_encoded
1.0    0.747774
0.0    0.252226
Name: proportion, dtype: float64
  </pre>
</section>

# Model Development
<section>
  <h3>1. Algoritma yang Digunakan: Random Forest dan Logistic Regression</h3>
  <p>
    Pada tahap awal pengembangan model, digunakan dua algoritma yaitu <strong>Random Forest</strong> dan <strong>Logistic Regression</strong>. Alasan pemilihan kedua algoritma ini adalah:
  </p>
  <ul>
    <li><strong>Random Forest:</strong> Algoritma ini kuat terhadap overfitting, mampu menangani data yang kompleks dan fitur yang banyak, serta memberikan interpretasi fitur penting (feature importance).</li>
    <li><strong>Logistic Regression:</strong> Model yang sederhana dan efektif untuk klasifikasi biner, mudah diinterpretasi, serta memberikan koefisien yang dapat digunakan untuk mengetahui pengaruh masing-masing fitur.</li>
  </ul>
  <p>
    Berikut adalah kode pembentukan model awal dengan parameter <code>class_weight='balanced'</code> untuk mengatasi ketidakseimbangan kelas:
  </p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
    
# Random Forest model with balancing
rf_model = RandomForestClassifier(class_weight='balanced', random_state=42)
rf_model.fit(X_train, y_train)

# Logistic Regression with balanced class weights
logreg_model = LogisticRegression(class_weight='balanced', random_state=42, max_iter=1000)
logreg_model.fit(X_train, y_train)
  </pre>
  <p>
    Parameter utama yang digunakan adalah:
  </p>
  <ul>
    <li><code>class_weight='balanced'</code>: untuk menyeimbangkan bobot kelas sehingga model tidak bias terhadap kelas mayoritas dan dapat belajar dengan baik pada kelas minoritas.</li>
    <li><code>random_state=42</code>: untuk memastikan hasil yang konsisten dan dapat direproduksi.</li>
    <li><code>max_iter=1000</code> pada Logistic Regression: untuk memastikan konvergensi model pada iterasi yang cukup.</li>
  </ul>

  <h3>2. Hyperparameter Tuning</h3>
  <p>
    <strong>Hyperparameter tuning</strong> adalah proses pencarian kombinasi parameter terbaik yang mengatur proses pelatihan model agar performa model optimal. Hyperparameter bukan parameter yang dipelajari oleh model, melainkan diatur sebelum pelatihan dimulai. Proses tuning biasanya melibatkan metode seperti grid search atau random search dengan validasi silang (cross-validation) untuk memilih parameter terbaik berdasarkan metrik evaluasi.
  </p>
  <p>Setelah dilakukan tuning, diperoleh parameter terbaik untuk masing-masing model:</p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Fitting 5 folds for each of 108 candidates, totalling 540 fits
Best RF Parameters: {'max_depth': None, 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 200}

Fitting 5 folds for each of 10 candidates, totalling 50 fits
Best Logistic Regression Parameters: {'C': 10, 'penalty': 'l1', 'solver': 'liblinear'}
  </pre>

  <h3>3. Model dengan 10 Most Important Features</h3>
  <p>
    <strong>Most important features</strong> adalah fitur-fitur yang memberikan kontribusi terbesar dalam pengambilan keputusan model. Pada <em>Random Forest</em>, penentuan fitur penting didasarkan pada kontribusi setiap fitur dalam mengurangi impurity (ketidakteraturan) pada proses pemisahan node di seluruh pohon keputusan. Fitur dengan nilai importance lebih tinggi menunjukkan seringnya fitur tersebut digunakan dan pengaruhnya yang besar terhadap prediksi.
  </p>
  <p>
    Sedangkan pada <em>Logistic Regression</em>, fitur penting ditentukan berdasarkan nilai koefisien model; koefisien yang lebih besar (positif atau negatif) menunjukkan pengaruh yang lebih signifikan terhadap probabilitas kelas target.
  </p>
  <p>Berikut adalah 10 fitur terpenting untuk masing-masing model:</p>

  <table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; margin-bottom: 1em;">
    <thead style="background-color: #f2f2f2;">
      <tr>
        <th>Feature (Random Forest)</th>
        <th>Importance</th>
        <th>Feature (Logistic Regression)</th>
        <th>Importance</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Curricular units 2nd sem (approved)</td><td>0.240282</td><td>Tuition fees up to date</td><td>2.533112</td></tr>
      <tr><td>Curricular units 2nd sem (grade)</td><td>0.137025</td><td>Curricular units 2nd sem (approved)</td><td>2.219088</td></tr>
      <tr><td>Curricular units 2nd sem (evaluations)</td><td>0.089054</td><td>Debtor</td><td>1.376592</td></tr>
      <tr><td>Curricular units 1st sem (evaluations)</td><td>0.080795</td><td>Gender</td><td>0.772013</td></tr>
      <tr><td>Course</td><td>0.067452</td><td>Displaced</td><td>0.638837</td></tr>
      <tr><td>Tuition fees up to date</td><td>0.053354</td><td>Scholarship holder</td><td>0.591102</td></tr>
      <tr><td>Father's occupation</td><td>0.049474</td><td>Curricular units 1st sem (evaluations)</td><td>0.375179</td></tr>
      <tr><td>Mother's occupation</td><td>0.043109</td><td>Curricular units 2nd sem (grade)</td><td>0.200681</td></tr>
      <tr><td>Application mode</td><td>0.040222</td><td>Curricular units 2nd sem (evaluations)</td><td>0.169265</td></tr>
      <tr><td>Mother's qualification</td><td>0.037606</td><td>Curricular units 2nd sem (enrolled)</td><td>0.125400</td></tr>
    </tbody>
  </table>
</section>

# Evaluation
<section>
  <p>
    Evaluasi model bertujuan untuk mengukur seberapa baik model dapat memprediksi kelas target dengan benar, terutama pada dataset yang tidak seimbang. Dalam penelitian ini, digunakan beberapa metrik evaluasi yaitu <strong>Balanced Accuracy</strong>, <strong>F1 Score</strong>, dan <strong>AUC Score</strong> untuk mendapatkan gambaran yang lebih komprehensif tentang performa model.
  </p>

  <h3>Metrik Evaluasi dan Rumusnya</h3>
  <ul>
    <li>
      <strong>Balanced Accuracy</strong>: Menghitung rata-rata recall (sensitivitas) dari setiap kelas, sehingga cocok untuk dataset yang tidak seimbang. Rumusnya adalah:
      <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-family: 'Consolas', 'Monaco', monospace;">
Balanced Accuracy = (Recall<sub>Positif</sub> + Recall<sub>Negatif</sub>) / 2
      </pre>
    </li>
    <li>
      <strong>Recall</strong> (Sensitivitas): Mengukur proporsi data positif yang berhasil diprediksi dengan benar. Rumusnya:
      <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-family: 'Consolas', 'Monaco', monospace;">
Recall = TP / (TP + FN)
      </pre>
      di mana TP = True Positives, FN = False Negatives.
    </li>
    <li>
      <strong>F1 Score</strong>: Harmonis rata-rata dari precision dan recall, memberikan keseimbangan antara keduanya, terutama penting saat data tidak seimbang. Rumusnya:
      <pre style="background:#23272e; color:#fff; padding:0.7em 1em; border-radius:6px; font-family: 'Consolas', 'Monaco', monospace;">
F1 = 2 × (Precision × Recall) / (Precision + Recall)
      </pre>
    </li>
    <li>
      <strong>AUC Score</strong> (Area Under the Curve): Mengukur kemampuan model membedakan antara kelas positif dan negatif melalui kurva ROC. Nilai AUC berkisar antara 0.5 (acak) hingga 1 (sempurna).
    </li>
  </ul>
  
<p>
  $$ \text{TPR} = \frac{TP}{TP + FN} $$
</p>
<p>
  $$ \text{FPR} = \frac{FP}{FP + TN} $$
</p>

  <h3>Confusion Matrix</h3>
  <p>Contoh confusion matrix untuk klasifikasi biner:</p>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
          Predicted
          0     1
Actual 0  TN    FP
       1  FN    TP
  </pre>
  <p>Keterangan:</p>
  <ul>
    <li><strong>TN</strong>: True Negative (kelas negatif yang diprediksi negatif)</li>
    <li><strong>FP</strong>: False Positive (kelas negatif yang diprediksi positif)</li>
    <li><strong>FN</strong>: False Negative (kelas positif yang diprediksi negatif)</li>
    <li><strong>TP</strong>: True Positive (kelas positif yang diprediksi positif)</li>
  </ul>

  <h3>Hasil Evaluasi Model</h3>

  <h4>1. Random Forest vs Logistic Regression (Binary Classification)</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Random Forest Performance:
Balanced Accuracy: 0.831
F1 Score: 0.931
AUC Score: 0.909

------------------------------------

Logistic Regression Performance:
Balanced Accuracy: 0.835
F1 Score: 0.902
ROC AUC Score: 0.894
  
  </pre>

  <h4>2. Random Forest vs Logistic Regression (Setelah Hyperparameter Tuning)</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Model Evaluation Results (After Hyperparameter Tuning):
                 Model  F1 Score  AUC Score  Balanced Accuracy
0        Random Forest     0.928      0.913              0.829
1  Logistic Regression     0.902      0.895              0.835
  </pre>

  <h4>3. Random Forest vs Logistic Regression (Model Terbaik dengan 10 Fitur Terpenting)</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
Final Model Comparison (Top 10 Features Only):
                                   Model  F1 Score  AUC Score  Balanced Accuracy
0        Random Forest (Top 10 Features)     0.932      0.893              0.841
1  Logistic Regression (Top 10 Features)     0.895      0.875              0.833
  </pre>
  <p>
    Berdasarkan hasil evaluasi, <strong>Random Forest</strong> dengan 10 fitur terpenting menunjukkan performa terbaik secara keseluruhan dengan nilai F1 Score tertinggi (0.932), balanced accuracy terbaik (0.841), dan AUC yang kompetitif (0.893). Meskipun Logistic Regression memiliki balanced accuracy sedikit lebih tinggi setelah tuning, Random Forest unggul dalam F1 Score yang lebih baik, yang berarti model ini lebih seimbang dalam memprediksi kelas positif dan negatif.
  </p>
  <p>
    Oleh karena itu, model Random Forest dengan 10 fitur terpenting dipilih sebagai model final karena kemampuannya yang lebih baik dalam menangani ketidakseimbangan kelas dan memberikan prediksi yang lebih akurat secara keseluruhan.
  </p>
</section>

# Kesimpulan
<section>
  <p>
    Model <strong>Random Forest</strong> secara konsisten menghasilkan nilai <em>F1 Score</em> dan <em>AUC Score</em> yang lebih tinggi, yang menunjukkan performa lebih baik dalam hal keseimbangan antara precision dan recall serta kemampuan perankingan.
  </p>
  <p>
    <em>Balanced Accuracy</em> sedikit lebih baik pada <strong>Logistic Regression</strong> ketika menggunakan seluruh fitur, namun <strong>Random Forest</strong> unggul saat hanya menggunakan 10 fitur teratas.
  </p>
  <p>
    Setelah dilakukan seleksi fitur, performa <strong>Random Forest</strong> meningkat lebih jauh dan mengungguli <strong>Logistic Regression</strong> pada semua metrik evaluasi.
  </p>

  <h3>Simulasi Klasifikasi Risiko Mahasiswa</h3>
  <p>
    Simulasi risiko dilakukan menggunakan 10 fitur terpenting berikut:
  </p>
  <ul>
    <li>Curricular units 2nd sem (approved)</li>
    <li>Curricular units 2nd sem (grade)</li>
    <li>Curricular units 2nd sem (evaluations)</li>
    <li>Curricular units 1st sem (evaluations)</li>
    <li>Course</li>
    <li>Tuition fees up to date</li>
    <li>Father's occupation</li>
    <li>Mother's occupation</li>
    <li>Application mode</li>
    <li>Mother's qualification</li>
  </ul>

  <h4>Parameter Transformasi Kebalikan Log dan Standard Scaling</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
original_stats = {
    'Curricular units 2nd sem (approved)': {'mean': 1.44, 'std': 1.44},
    'Curricular units 2nd sem (grade)': {'mean': 2.56, 'std': 0.64},
    'Curricular units 2nd sem (evaluations)': {'mean': 1.63, 'std': 0.69},
    'Curricular units 1st sem (evaluations)': {'mean': 1.70, 'std': 0.67}
}

def inverse_transform(value, mean, std):
    return np.expm1((value * std) + mean)
  </pre>

  <p>
  </p>

  <h4>Ambang Batas Klasifikasi Risiko</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
thresholds = {
    'Curricular units 2nd sem (approved)': [4, 2],  # ≥4 = Safe, ≥2 = Moderate, <2 = At Risk
    'Curricular units 2nd sem (grade)': [14.0, 10.0],
    'Curricular units 2nd sem (evaluations)': [6, 3],
    'Curricular units 1st sem (evaluations)': [6, 3],
    'Course': [[33, 171, 999], [8012, 9999]],  # Safe and Moderate course IDs
    'Tuition fees up to date': [[1], [0]],  # 1 = Up-to-date (Safe), 0 = Not (Moderate)
    "Father's occupation": [[3, 4, 5], [1, 2]],
    "Mother's occupation": [[3, 4, 5], [1, 2]],
    'Application mode': [[1, 2], [5, 6]],
    "Mother's qualification": [[4, 5], [2, 3]]  # 4 = Bachelor's, 5 = Master's
}
  </pre>

  <p>
    Berdasarkan ambang batas ini, setiap fitur diklasifikasikan menjadi kategori <em>Safe</em>, <em>Moderate</em>, atau <em>At Risk</em>, lalu digabungkan untuk menentukan risiko keseluruhan mahasiswa.
  </p>

  <h4>Hasil Klasifikasi Risiko</h4>
  <pre style="background:#f4f4f4; padding:1em; border-radius:6px;">
📊 Risk Classification Summary:
Overall_Risk
High Risk        1493
Moderate Risk     192
Name: count, dtype: int64
  </pre>

  <p>Contoh data mahasiswa dengan klasifikasi risiko:</p>
  <table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; margin-bottom: 1em;">
    <thead style="background-color: #f2f2f2;">
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
      <tr><td>10.68</td><td>20.88</td><td>1.54</td><td>1.82</td><td>9.0</td><td>0.0</td><td>3.0</td><td>3.0</td><td>4.0</td><td>0.0</td><td>High Risk</td></tr>
      <tr><td>5.28</td><td>11.26</td><td>8.28</td><td>4.64</td><td>13.0</td><td>1.0</td><td>3.0</td><td>5.0</td><td>6.0</td><td>16.0</td><td>Moderate Risk</td></tr>
      <tr><td>10.68</td><td>15.25</td><td>1.54</td><td>6.53</td><td>1.0</td><td>1.0</td><td>9.0</td><td>9.0</td><td>8.0</td><td>15.0</td><td>High Risk</td></tr>
      <tr><td>10.68</td><td>25.83</td><td>2.76</td><td>4.64</td><td>8.0</td><td>1.0</td><td>9.0</td><td>9.0</td><td>0.0</td><td>0.0</td><td>High Risk</td></tr>
    </tbody>
  </table>
  <p>
    Kinerja akademik, khususnya pada semester kedua, dikombinasikan dengan status keuangan dan latar belakang keluarga, merupakan faktor utama dalam memprediksi risiko mahasiswa untuk dropout. Informasi ini dapat membantu fokus intervensi pada mahasiswa yang mengalami kesulitan akademik maupun tantangan finansial dan sosial.
  </p>
  <p>
    Mahasiswa dengan jumlah evaluasi yang rendah atau tidak konsisten serta tingkat kelulusan yang rendah cenderung diklasifikasikan sebagai <strong>High Risk</strong>.
  </p>
  <p>
    Bahkan mahasiswa dengan nilai yang relatif tinggi (misalnya mahasiswa nomor 8 dengan nilai rata-rata 25.83) dapat dikategorikan berisiko tinggi jika faktor lain seperti evaluasi, jurusan, atau latar belakang orang tua menunjukkan potensi masalah.
  </p>
  <p>
    Mahasiswa dengan catatan akademik yang lebih seimbang dan pembayaran biaya kuliah yang lancar (misalnya mahasiswa nomor 3) diklasifikasikan sebagai <strong>Moderate Risk</strong>, menunjukkan bahwa status pembayaran dan partisipasi akademik (evaluasi) berperan penting dalam menurunkan tingkat risiko.
  </p>
</section>
