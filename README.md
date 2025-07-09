# eda-dataset
## Backgroud
Dalam dunia analisis data, ketersediaan data dalam jumlah besar tidak serta-merta menjamin diperolehnya informasi yang bermakna. Data mentah sering kali mengandung berbagai masalah seperti nilai yang hilang, duplikasi, anomali, dan pola yang tidak terlihat secara langsung. Oleh karena itu, diperlukan proses Exploratory Data Analysis (EDA) sebagai tahap awal untuk memahami struktur dan kualitas data sebelum dilakukan analisis lanjutan atau pemodelan. Melalui EDA kita dapat memahami struktur dan kualitas data sebelum modeling, Menemukan pola, tren, dan anomali dalam data, menentukan metode analisis yang tepat, dan meningkatkan keakuratan hasil analisis dan prediksi. Contoh kasus dataset https://www.kaggle.com/datasets/eswaranmuthu/u-s-economic-vital-signs-25-years-of-macro-data/code

## Version Libraries
- pandas
- missing value
  
## Insight
1. Membaca data set
   Mengimport library pandas untuk membaca dataset
    import pandas as pd
    baca dataset csv menggunakan syntax pd.read_csv()
    df = pd.read_csv('/content/tugas_dev.csv')
   
2. Ringkasan data
   info() : berguna untuk memahami dengan cepat struktur dan konten DataFrame, membantu dalam eksplorasi dan persiapan data
   df.info()
   Range index data entries harus sesuai dengan jumlah column yang ada dalam seluruh data, jika tidak sesuai maka ada data yang hilang
    
3. Missing Value
- Mengecek missing value
    df.isna().sum()
   Berdasarkan informasi yang diperoleh ditemukan data yang hilang pada kolom SOFR (contoh kasus dalam dataset)
- Mengecek statistical summary
  df.describe()
  untuk data statistical summary yang akan muncul hanya data dalam bentuk numerik, sehingga dalam bentuk object (string) tidak akan muncul
- Mengecek data string
  df['Date'].describe()
  date merupakan data type object sehingga tidak muncul angka, yand ada hanya nilai count, unique (data yang tidak berulang), top (nilai mode) dan freq (nilai frekuensi dari modusnya)
- nilai mean mendekati 50% maka terdapat data terdistribusi secara normal
- jika terdapat kolom yang boolean/biner karena nilainya 0 atau 1, hanya perlu melakukan keseimbangan data. jika nilai jauh kurang/lebih dari 50% maka data tidak balance. sehingga akan terjadi permasalahan dalam prediksa data menggunakan machine learning. hal yang perlu dilakukan adalah menambah atau mengurangi data agar seimbang.
- Mengatasi nilai missing value
  for column in df.columns:
    if df[column].dtype == 'object':
        # Jika kolom bertipe object, isi dengan mode
        df[column].fillna(df[column].mode()[0], inplace=True)
    else:
        # Jika kolom bertipe numerik, isi dengan mean
        df[column].fillna(df[column].mean(), inplace=True)
  
4. Mengatasi duplikat data
- Mengecek apakah ada duplicate di seluruh kolom
  check_duplicate = df.duplicated().sum()
  print(f"Jumlah data yang duplikat = {check_duplicate}")
- Handling duplicate
  df = df.drop_duplicates()
- Mengecek duplicate setelah di-handle
  handle_duplicate = df.duplicated().sum()
  print(f"Jumlah data yang duplikat = {handle_duplicate}")

  ## Advice
  tugas ini bisa di improve ke machine learning

  #EDA #python #ML
  follow: @devia_sari51
