### 🚀 Ingest data dari jupyter notebook (linux mint)

### 🚀 import csv dengan pandas dan sqlalchemy 

- saya telah membuat database di mysql dengan nama ```ingest_data_terminal```
- silahkan buat database terlebih dahulu di terminal

  
- saya asumsikan sudah install python dan jupyter notebook
- setelah itu download ```Netflix Userbase.csv``` di repo ini atau download di [kaggle](https://www.kaggle.com/datasets/arnavsmayan/netflix-userbase-dataset) 
- panggil jupyter notebook di terminal ``` jupyter notebook ``` dan klik new ```python3 (ipykernel)``` di pojok kanan atas
- import library python berikut di jupyter notebook
  ```
  import csv
  import MySQLdb
  import pandas as pd
  from sqlalchemy import create_engine
  ```
- baca file csv dan buat variable dataframe
  ```
  df = pd.read_csv ('Netflix Userbase.csv')
  ```
- pastikan penulinsan file_name.csv benar
- mengetahui bahwa csv telah masuk ke dataframe, tampilkan dataframe dengan menggunakan
  ```
  df.head (5)
  ```

![Screenshot from 2023-08-17 20-11-27](https://github.com/agilsaputra/Ingest_data/assets/22126819/ef659b53-db19-41e4-aa70-013a0e15b392)

- generate schema buat table ``` 'Ingest_Jupyter' ``` adalah nama tabel saya
  
  ```
  print(pd.io.sql.get_schema(df, 'Ingest_Jupyter'))
  ```
  hasilnya berikut
  ```
  CREATE TABLE "Ingest_Jupyter" (
  "User ID" INTEGER,
  "Subscription Type" TEXT,
  "Monthly Revenue" INTEGER,
  "Join Date" TEXT,
  "Last Payment Date" TEXT,
  "Country" TEXT,
  "Age" INTEGER,
  "Gender" TEXT,
  "Device" TEXT,
  "Plan Duration" TEXT)
  ```

- seletah itu koneksikan ke mysql menggunakan sqlalchemy dengan syntax berikut
 ```
mysql_engine = create_engine("mysql://user:password@localhost:port/database")
```
- isikan ```user,password,port,database ``` sesuai dengan database kalian
- in case punya saya yaitu
```
mysql_engine = create_engine("mysql://admin1:818642@localhost:3306/ingest_data_terminal")
```
-lalu connect engine alchemy ke mysql
```
mysql_engine.connect
```
-buat variable tabel dan eksekusi dari dataframe ke sql
```
table_name = 'Ingest_Jupyter'
df.to_sql(name='Ingest_Jupyter',con=mysql_engine, if_exists='replace')
```
output

![Screenshot from 2023-08-17 20-24-31](https://github.com/agilsaputra/Ingest_data/assets/22126819/d20951f5-d48f-42bf-b136-ac46003651dd)

- 2500 adalah total row dalam database yang telah di masukkan   
🚀🚀selamat file csv sudah masuk kedalam database mysql 🚀🚀
