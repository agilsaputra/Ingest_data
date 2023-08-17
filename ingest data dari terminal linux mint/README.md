## :rocket: Ingest data :rocket: 🧑‍💻 


#### Import csv data kedalam my sql menggunakan terminal linux 📄 :point_right:  🧑‍💻 

- install mysql di terminal menggunakan ```sudo apt install mysql-server``` (saya menggunakan debian base linux)   
- buka terminal dan login mysql ```sudo mysql -u root```   
- buat database baru dengan ```CREATE DATABASE ingest_data_terminal;```   
- pastikan query berjalan dan tampilkan dengan ```SHOW DATABASES;```   
```
+----------------------+
| Database             |
+----------------------+
| coba                 |
| information_schema   |
| ingest_data_terminal |
| mysql                |
| performance_schema   |
| sys                  |
| test                 |
| wordpress            |
+----------------------+
``` 
- gunakan database yang baru dibuat  ```USE ingest_data_terminal;```    
- buat tabel baru      
```
CREATE TABLE ingest_data_terminal (
      User_ID INT,
      Subscription_Type VARCHAR(255),
      Monthly_Revenue INT,
      Join_Date DATE,
      Last_Payment_Date DATE,
      Country VARCHAR(255),
      Age INT,
      Gender VARCHAR(255),
      Device VARCHAR(255),
      Plan_Duration VARCHAR(255)
);
```     
- setelah itu download ``` Netflix Userbase.csv ``` di repo ini atau download di kaggle ```https://www.kaggle.com/datasets/arnavsmayan/netflix-userbase-dataset ```     
- ingest data dengan menggunakan ```LOAD DATA INFILE```, cek file ```secure_file_priv``` dengan menggunakan query ```SHOW VARIABLES LIKE 'secure_file_priv';```     
```
+------------------+-----------------------+
| Variable_name    | Value                 |
+------------------+-----------------------+
| secure_file_priv | /var/lib/mysql-files/ |
+------------------+-----------------------+
1 row in set (0,03 sec)
```     
- folder secure_file_priv yang di boleh kan oleh mysql untuk mengupload file atau bisa di non aktifkan tp sy mengunakan metode copy file kedalam  ```/var/lib/mysql-files/ ```.
- copy file csv dari folder download ke dalam ```/var/lib/mysql-files/ ``` (akan berbeda jika menggunakan windows patch filenya)    

- setelah itu jalankan query ```LOAD DATA INFILE``` dengan syntax      
```
LOAD DATA INFILE '/var/lib/mysql-files/Netflix Userbase.csv'#ganti patch folder dengan secure_file_priv anda dan file_name.csv
INTO TABLE Netflix_Userbase #nama table yang dibuat
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```      
- seletah itu tampilkan table dengan ``` SELECT * FROM Netflix_Userbase; ```    

![Screenshot from 2023-08-17 14-40-28](https://github.com/agilsaputra/Ingest_data/assets/22126819/e47546f8-f110-4441-8894-a82bdfaeae49)

- 🚀 selamat data csv berhasil di masukan kedalam sql :tada: :sparkles: :sparkles: 

