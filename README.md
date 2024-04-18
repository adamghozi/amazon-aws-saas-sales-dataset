# Amazon AWS SaaS Sales Dataset
### Adam Ghozi Rahman

- Jupyter notebook: **AWS Profit Data Analysis.ipynb**
- data set: **AWS SaaS-Sales.csv**

# Table of contents
1. [Pendahuluan](#introduction)

2. [Deskripsi dari data set](#section2)
   1. [Statistik Deskriptif](#sec2p1)
   2. [Missing Value dan Outlier](#sec2p2)
   3. [Penambahan Kolom](#sec2p3)

3. [Data Analysis](#section3)
   1. [Uji Normaltest](#sec3p1)
   2. [Uji Korelasi Spearman](#sec3p2)
   3. [Profit Paling Rendah Berdasarkan `Subregion` dan `Product`](#sec3p3)

4. [Kesimpulan Data Analysis](#section4)

5. [Referensi](#section5)
   
  
## 1. Pendahuluan <a name="introduction"></a>
- README ini menjelaskan pekerjaan yang dilakukan pada set data AWS SaaS Sales. Sumber daya yang digunakan termasuk Python dan paket terkait Jupyter, matplotlib, Seaborn, statsmodels, dan SciPy. Semua paket ini disertakan sebagai bagian dari distribusi Anaconda Python.
- Analisis ini berbentuk satu notebook Jupyter dengan nama file yang diberikan di atas. Untuk melihat file ini, unduh dari repositori ini dan mulai notebook Jupyter di folder yang berisi file tersebut. Gunakan perintah Jupyter notebook pada baris perintah.
- Semua gambar yang dimaksudkan untuk disertakan dalam README ini berada di subdirektori images dari repositori ini.

##  2. Data Understanding dan Cleaning <a name="section2"></a>
Dataset yang disediakan berisi data transaksi dari perusahaan Software as a Service (SaaS) yang berspesialisasi dalam perangkat lunak penjualan dan pemasaran untuk klien bisnis ke bisnis (B2B). Setiap baris dalam dataset mewakili satu transaksi atau pesanan, dengan total 9.994 transaksi. Dataset ini terdiri dari berbagai kolom, termasuk ID Baris (Row ID) sebagai identifikasi unik untuk setiap transaksi, ID Pesanan (Order ID) sebagai identifikasi unik untuk setiap pesanan, Tanggal Pesanan (Order Date) sebagai tanggal pesanan, dan berbagai atribut lainnya seperti nama kontak, negara, kota, wilayah, subwilayah, nama pelanggan, ID pelanggan, industri, segmen pelanggan, produk, lisensi, total penjualan, jumlah barang, diskon, dan keuntungan. Dataset ini memberikan informasi yang komprehensif tentang transaksi penjualan perusahaan, termasuk detail tentang pelanggan, produk, jumlah penjualan, diskon, dan keuntungan, memungkinkan untuk analisis mendalam tentang kinerja perusahaan, perilaku pelanggan, dan tren pasar.

## 2.1 Statistik Deskriptif <a name="sec2p1"></a>
Fungsi **describe()** dari library pandas dapat menunjukkan ringkasan penting tentang statistika deskriptif data set.

foto describe()

- Dataset ini terdiri dari 9994 baris, dengan rata-rata Row ID sebesar 4997,5 dan standar deviasi sebesar 2885,16.
- Tanggal bervariasi dari 1 Januari 2020 hingga 31 Desember 2023.
- ID Pelanggan berkisar dari 1001 hingga 1101, dengan rata-rata sebesar 1049,77 dan standar deviasi sebesar 29,72.
- Data Penjualan menunjukkan rata-rata nilai transaksi sebesar $1049,77, dengan nilai minimum sebesar $0,44 dan maksimum sebesar $22638,48.
- Jumlah barang yang dijual per transaksi memiliki rata-rata sebesar 229,86 dan standar deviasi sebesar 623,25, dengan rentang dari 0,44 hingga 22638,48.
- Diskon yang diterapkan pada transaksi memiliki rata-rata sebesar 3,79, dengan standar deviasi sebesar 2,23 dan rentang dari 1 hingga 14.
- Keuntungan yang dihasilkan dari transaksi memiliki rata-rata sebesar $28,66, dengan standar deviasi sebesar $234,26, dengan rentang dari -$6599,98 hingga $8399,98.
- Berbagai atribut seperti ID Pesanan, Tanggal Pesanan, Nama Kontak, Negara, Kota, Wilayah, Subwilayah, Pelanggan, Industri, Segmen, Produk, dan Lisensi menunjukkan tingkat keunikan yang berbeda, dengan nilai teratas dan frekuensi sebagaimana dijelaskan dalam ringkasan yang disediakan.

## 2.2 Missing Value dan Outlier <a name="sec2p2"></a>
Perlu dilakukan pengecekan terhadap `missing value` dan `outlier` dalam data set yang dapat mengganggu analisis data.

Dari data set, tidak ditemukan data NaN atau `missing value` dan tidak ada outlier yang tidak diperlukan dalam analisis, maka tidak dilakukan data cleaning.

## 2.3 Penambahan Kolom <a name="sec2p3"></a>

Selanjutnya, perlu ditambahkan kolom `datetime` pada dataset agar disaat analisis dapat melihat tren dari data. hal ini dilakukan dengan menggunakan kolom `Date Key`.

# 3. Data Analysis <a name="section3"></a>

Setelah melakukan tahap Data Cleaning. Sekarang, data siap untuk dianalisis untuk mencari tahu bagaimana pengaruh `Profit` dengan `Sales`, `Quantity` dan `Discount`. 

## 3.1 Uji Normaltest <a name="sec3p1"></a>

Perlu dilakukan uji normaltest untuk menentukan uji parametrik atau non parametrik yang akan digunakan pada analisis selanjutnya. Berikut adalah hasil dari uji normaltest dari kolom `Sales`, `Quantity`, `Discount` dan `Profit`.

Sales: Statistics=18033.308, p-value=0.000
Sales is not normally distributed (reject H0)

Quantity: Statistics=2148.018, p-value=0.000
Quantity is not normally distributed (reject H0)

Discount: Statistics=2977.822, p-value=0.000
Discount is not normally distributed (reject H0)

Profit: Statistics=14363.736, p-value=0.000
Profit is not normally distributed (reject H0)

Hasil diatas menunjukkan bahwa keempat kolom diatas memiliki data yang tidak terdistribusi normal. Maka, untuk selanjutnya perlu dilakukan uji non-parametrik.

## 3.2 Uji Korelasi Spearman <a name="sec3p2"></a>

Perlu dilakukan uji korelasi antara `Profit` dengan `Sales`, `Quantity` dan `Discount` untuk melihat apakah ada korelasi kuat antara kolom tersebut

Spearman's correlation coefficient antara Sales dan Profit: 0.5184066611400607
Spearman's correlation coefficient antara Quantity dan Profit: 0.2344912031227869
Spearman's correlation coefficient antara Discount dan Profit: -0.5433501822306211

Berdasarkan hasil diatas, 
* antara Sales dan Profit memiliki hubungan yang moderat dan positif,
* antara Quantity dan Profit memiliki hubungan yang lemah dan positif,
* antara Discount dan Profit memiliki hubungan yang moderat dan negatif.

## 3.3 Profit Paling Rendah Berdasarkan `Subregion` dan `Product` <a name="sec3p3"></a>

Berdasarkan hasil analisis, profit paling rendah adalah pada `Subregion` ANZ dan JAPN. sementara pada kedua `Subregion` tersebut `Product` dengan profit paling rendah adalah ContactMatcher. Selanjutnya dilakukan uji korelasi koefisien antara `Profit` dan `Discount` dikalikan dengan `Sales` pada `Subregion` ANZ dan JAPN dengan `Product` ContactMatcher, berikut hasil uji korelasinya.

Spearman's correlation coefficient antara Discount*Sales dan Profit di `Subregion` ANZ: -0.9603105960173816
Spearman's correlation coefficient antara Discount*Sales dan Profit di `Subregion` JAPN: -0.904091425332207

Berdasarkan hasil tersebut, dapat disimpulkan bahwa antara `Profit` dan `Discount` dikalikan dengan `Sales` memiliki korelasi yang sangat kuat dan negatif.

## 4. Kesimpulan Data Analysis <a name="section4"></a>

Kesimpulan utama adalah sebagai berikut
1. `Profit`:
    - Rata-rata: 28.66
    - Standar Deviasi: 234.26
    - Minimum: -6599.98
    - Median: 8.67
    - Maximum: 8399.98
2. `Sales`:
    - Rata-rata: 229.86
    - Standar Deviasi: 623.25
    - Minimum: 0.44
    - Median: 54.49
    - Maximum: 22638.58
3. `Discount`:
    - Rata-rata: 0.16
    - Standar Deviasi: 0.21
    - Minimum: 0.00
    - Median: 0.20
    - Maximum: 0.80
4. Korelasi antara `Profit` dan `Discount` dikalikan dengan `Sales` pada `Subregion` ANZ dan JAPN dengan `Product` ContactMatcher adalah -0.96 pada `Subregion` ANZ dan 0.90 pada `Subregion` JAPN.

## 5. Referensi <a name="section5"></a>

- [1]  Anaconda Distribution
https://www.anaconda.com/

- [2] Python Software Foundation
https://www.python.org/

- [3] Project Jupyter
https://jupyter.org/

- [4] Sharing Jupyter notebooks
https://nbviewer.jupyter.org/

- [5] pandas: Python data analysis library
https://pandas.pydata.org/

- [6] numpy: The fundamental package for scientific computing with Python
https://numpy.org/

- [7] seaborn: statistical data visualization
https://seaborn.pydata.org/index.html#

- [8] matplotlib: Python plotting library
https://matplotlib.org/

- [9] plotly: low-code python data Apps
https://plotly.com/

- [10] Amazon AWS SaaS Sales Dataset
https://www.kaggle.com/datasets/nnthanh101/aws-saas-sales

- [11] IPython
https://ipython.org/

- [12] statsmodels: Statistics in Python
https://www.statsmodels.org/stable/index.html

- [13] scipy.stats : Statistics with SciPy
https://docs.scipy.org/doc/scipy/reference/tutorial/stats.html
