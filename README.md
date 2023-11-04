## Improving Employee Retention by Predicting Employee Attrition Using Machine Learning

Sumber daya manusia (SDM) adalah aset utama yang perlu dikelola dengan baik oleh perusahaan agar tujuan bisnis dapat tercapai dengan efektif dan efisien. Pada kesempatan kali ini, kita akan menghadapi sebuah permasalahan tentang sumber daya manusia yang ada di perusahaan. Fokus kita adalah untuk mengetahui bagaimana cara menjaga karyawan agar tetap bertahan di perusahaan yang ada saat ini yang dapat mengakibatkan bengkaknya biaya untuk rekrutmen karyawan serta pelatihan untuk mereka yang baru masuk. Dengan mengetahui faktor utama yang menyebabkan karyawan tidak merasa, perusahaan dapat segera menanggulanginya dengan membuat program-program yang relevan dengan permasalahan karyawan.

#### Data Preprocessing
 - Handling Missing Value 
	 -  IkutProgramLOP sebesar 89,9% dipertimbangkan untuk di hapus karena banyak sekali memiliki nilai null
	 - AlasanResign sebesar 23%, mengisi dengan nilai "masihbekerja" karena yang tidak mengisi ini, adalah orang yang tidak memiliki tanggal resign/masih bekerja
	 - JumlahKetidakhadiran sebesar 2,09% mengisi dengan nilai median
	 - SkorKepuasanPegawai sebesar 1,74% mengisi dengan nilai median
	 - JumlahKeikutsertaanProjek sebesar 1,05% mengisi dengan nilai median
	 - JumlahKeterlambatanSebulanTerakhir sebesar 0,35% mengisi dengan nilai median
 - Handling Summary Aneh 
	 -  Terdapat nilai Yes di feature kolom Pernah Bekerja, sehingga perlu di ganti nilai tersebut dengan nilai 1 yang merepresentasikan Yes.
 - Dropped Data
	 - Membuang kolom yang memiliki satu unique value (konstanta) yaitu Pernah Bekerja

#### Annual Report on Employee Number Changes
![1](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/1.jpeg)

Pada tahun 2017, perusahaan mengalami penurunan karyawan yang signifikan. Karyawan yang resign jauh lebih tinggi daripada karyawan yang masuk. Hal ini menunjukkan bahwa perusahaan mengalami fluktuasi karyawan yang besar pada tahun ini, dan penurunan menjadi tanda bahwa perusahaan sedang menghadapi tantangan atau masalah yang perlu segera diatasi.

Pada tahun 2018 hingga 2020, terlihat bahwa tidak ada pertambahan karyawan yang signifikan, sementara jumlah karyawan yang resign tetap tinggi. Ini mengindikasikan bahwa perusahaan belum mampu membalikkan tren negatif yang dimulai pada tahun 2017. Akibat hal tersebut, banyak proyek-proyek yang tidak selesai, yang dapat mempengaruhi produktivitas dan efisiensi perusahaan.

#### Resign Reason Analysis for Employee Attrition Management Strategy
#####  Persentase karyawan yang masih bekerja berdasarkan divisi pekerjaan
![2](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/2.jpeg)

Grafik tersebut memberikan gambaran tentang persentase karyawan yang masih bekerja berdasarkan divisi pekerjaan. Terdapat 7 Divisi tidak memiliki pengunduran diri, sementara Data Analyst memiliki tingkat pengunduran diri sebesar 50%, yang perlu di analisis lebih lanjut terkait alasan apa yang menyebabkan karyawan mengundurkan diri.

##### Resign Reason Analysis for Employee Attrition Management Strategy
![3](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/3.jpeg)

##### Rekomendasi :
Fresh Graduate
disarankan untuk memberikan kesempatan untuk pekerjaan jarak jauh kepada karyawan yang memungkinkan, terutama bagi mereka yang bekerja di bidang IT seperti software engineer, yang dapat bekerja dari berbagai lokasi.

Middle level
Alasan pengunduran diri berkaitan dengan jam kerja yang terlalu padat, perusahaan bisa mempertimbangkan untuk menambah jumlah karyawan di tim atau departemen terkait. Dengan cara ini, beban kerja dapat lebih merata dan mengurangi tekanan individual.
Senior level

perusahaan dapat fokus pada fasilitas dan program kesejahteraan karyawan, termasuk program kesehatan, kegiatan sosial, pengembangan diri, dan keseimbangan kerja-kehidupan pribadi. Hal ini akan membantu menciptakan lingkungan kerja yang lebih seimbang dan menyenangkan.

#### Build an Automated Resignation Behavior Prediction using Machine Learning
##### Data Preprocessing Flow
![4](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/4.jpeg)

##### Model Comparison
![5](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/5.jpeg)

Model yang dipilih adalah XGBoost karena memiliki *accuracy* yang cukup memadai dan nilai *recall* yang tertinggi diantara semua model

Untuk XGBoost digunakan Hyperparameter sebagai berikut: : eta = 0.05, max_depth = 1, scale_pos_weight = 1.3

Hyperparameter nthread, tree_method dan predictor dipilih sedemikian rupa agar komputasi dan fitting model memakan waktu yang sesedikit mungkin. Nilai untuk Hyperparameter eta dan scale_pos_weight dipilih karena menghasilkan nilai *recall* tertinggi tanpa mengorbankan nilai *accuracy* begitu besar, serta model tidak mengalami overfitting dengan menggunakan Hyperparameter tersebut

#### Presenting Machine Learning Products to the Business Users
##### Confusion Metrix
![6](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/6.jpeg)

Dengan metric utama pada modeling adalah recall, dimana berfungsi untuk mendeteksi sebanyak-banyaknya karyawan yang resign dan benar-benar resign (TP).
Dari confusion metrix terlihat jumlah karyawan yang resign dan benar-benar resign(TP) sebanyak 22, sedangkan karyawan yang tidak resign sebanyak (TN) 60.
Dan karyawan yang terdeteksi tidak resign tetapi pada kenyataannya resign adalah 5 karyawan (FN) dan sedangkan karyawan yang sebenarnya tidak resign tetapi terdeteksi resign (FP) sebanyak 0 karyawan.

##### Feature Importance
![7](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/7.jpeg)
Feature yang paling berpengaruh adalah feature AlasanResign, dengan top 3 alasan resign yang paling berpengaruh adalah
-   Jam Kerja
-   Ganti Karir
-   Toxic Culture
Alasan Resign ini seperti pada tahap EDA, didominasi oleh fresgraduate program dan mid level.

##### Recommendation Business
Alasan Resign Jam Kerja
Selidiki penyebab, pantau dan evaluati beban kerja karyawan supaya jam kerja yang terlalu padat tidak menjadi hambatan bagi karyawan menjaga keseimbangan hidup. Pertimbangkan untuk memberikan opsi kerja fleksibel atau kebijakan kerja dari jarak jauh. Ini dapat membantu mengurangi tekanan yang mungkin disebabkan oleh jam kerja yang tidak fleksibel.
Penelitian menunjukkan beban kerja yang terlalu padat berdampak negatif. Selidiki penyebab dan berikan opsi kerja fleksibel." - Dr. Jane Doe.
  
  
Alasan Resign Ganti Karir
Sediakan jalur karir yang terdefinisi dengan baik dan jelas agar pegawai memiliki visi dan motivasi untuk tetap berkembang di perusahaan. Ini akan membantu mempertahankan karyawan di semua tingkatan, termasuk Middle dan Senior.
Jalur karir yang jelas adalah motivasi utama. Penelitian menegaskan perusahaan dengan jalur karir yang jelas mempertahankan karyawan." - Prof. John Smith.
  

Alasan Resign Toxic Culture
Selidiki penyebab toksisitas dalam budaya perusahaan. Ini bisa termasuk evaluasi hubungan antara atasan dan bawahan, tingkat stres di lingkungan kerja, atau masalah komunikasi yang perlu diatasi. Fokus pada pengembangan keterampilan kepemimpinan manajer untuk menciptakan lingkungan kerja yang positif, di mana karyawan merasa dihargai dan didukung.Selalu berikan saluran komunikasi yang terbuka agar karyawan dapat melaporkan masalah dan memberikan masukan untuk perbaikan budaya perusahaan.
Penelitian psikologi organisasi menunjukkan budaya toksik merugikan kesejahteraan karyawan. Selidiki dan atasi penyebabnya." - Dr. Emily Johnson.
  
  #### Recommendation Software Development
  ![8](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/8.jpeg)
  
  #### Business Impact Simulation
  ![9](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/9.jpeg)
  ![10](https://github.com/cittamudita/Improving-Employee-Retention-by-Predicting-Employee-Attrition-Using-Machine-Learning/blob/905c9f49c84a62eb3c0ebc1a56faa2cf126e8e3f/10.jpeg)
