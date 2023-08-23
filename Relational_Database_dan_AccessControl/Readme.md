### 🔖 Relasi Database Mysql dan Control User access dan role 👥 🧑‍💻

#### 📊 Relasi database Contoh skema database toko online
- Relasi database ini menggunakan database [ini](https://github.com/agilsaputra/Ingest_data_dan_querySQL/blob/master/Relational_Database_dan_AccessControl/DB_relasi.sql)
- Schema tabel dapat dilihat berikut
  ![Screenshot from 2023-08-23 20-40-21](https://github.com/agilsaputra/Ingest_data_dan_querySQL/assets/22126819/9d470877-1a72-4b1e-b79e-61fba9121122)

- Penjelasan relasi tabel yang dibuat
   - 📑 Tabel ```Product```
       ```
       CREATE TABLE Products (
         product_id INT AUTO_INCREMENT PRIMARY KEY,
         name VARCHAR(100),
         price DECIMAL(10, 2)
       );

       ```

   - Tabel Product memiliki 1 buah primary key dan tidak mempunyai foregin key, kolom harga maks 10 digit dan 2 angka dr belakang adalah desimal
   - **Note** : semua ```PRIMARY KEY``` yang dibuat adalah mengunakan **AUTO_INCREMENT** yaitu otomatis dan nilainya bertambah

   - 📑 Tabel ```Customers```
     ```
     CREATE TABLE Customers (
       customer_id INT AUTO_INCREMENT PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       email VARCHAR(100)
     );
     ```
   - Tabel ```Customers``` juga memiliki 1 buah PRIMARY KEY dan tidak punya Foreign key

   - 📑 Tabel ```Addresses```
     ```
     CREATE TABLE Addresses (
      address_id INT AUTO_INCREMENT PRIMARY KEY,
      customer_id INT,
      street VARCHAR(100),
      city VARCHAR(50),
      state VARCHAR(50),
      FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
     );
     ```
   - Tabel ```Addresses``` memupnyai 1 PRIMARY KEY DAN 1 FOREIGN KEY, Foreign key disini menghubungkan antara tabel ```Addresses``` dengan tabel ```Costumers```
     dengan memakai ```customer_id```
   
   - 📑 Tabel ```Orders```
     ```
     CREATE TABLE Orders (
       order_id INT AUTO_INCREMENT PRIMARY KEY,
       customer_id INT,
       order_date DATE,
       FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
     );
     ```
   - Tabel ```Orders``` juga memiliki 1 PK DAN FK, Foreign key tabel ```Order``` menggubungkan tabel ```orders``` dengan tabel ```customers```
     dengan memakai ```customer_id```

   - 📑 Tabel ```Order_Items```
     ```
     CREATE TABLE Order_Items (
      order_item_id INT AUTO_INCREMENT PRIMARY KEY,
      order_id INT,
      product_id INT,
      quantity INT,
      price_per_unit DECIMAL(10, 2),
      FOREIGN KEY (order_id) REFERENCES Orders(order_id),
      FOREIGN KEY (product_id) REFERENCES Products(product_id)
     );
     ```
  
   - Tabel ```Order_Items``` mempunyai 1 PK dan 2 FK, Foreign key disini mengubungkan antara tabel ```Order_item``` dg ```Orders``` dan ```Product``` dengan menggunakan order_id dan product_id

#### 🔃 Identifikasi constraint 
  - Pembuatan database Schema diatas sudah berelasi antar tabel tapi nama ```constraint``` di generate otomatis oleh mysql jika 1 tabel memiliki 2 foreign key maka nantinya akan membingungkan    
      
    ***case***
    
    ![Screenshot from 2023-08-22 21-38-14](https://github.com/agilsaputra/Ingest_data_dan_querySQL/assets/22126819/236b48dd-d3ba-4561-a342-ade58ff6046f)

    - Tabel ```Order_Items``` diatas mempunyai relasi ke tabel ```Orders``` dan ```Products```, yang mana tabel ```Order_Items``` mempunyai 2 FOREGIN KEY ke tabel ```Orders``` dan ```Products```. dan memiliki nama ```constraint``` yang hampir sama karena kita tidak menambahkan di awal query. Nama ```constraint``` yang sama atau acak nantinya akan menyulitkan jika terjadi error saat query atau error database.     
      ***Perbedaan create table sebelum memberi nama constrain dan sesudah***
      ***query create tabel Order_Items yang lama***
          
      ```
      CREATE TABLE Order_Items (
        order_item_id INT AUTO_INCREMENT PRIMARY KEY,
        order_id INT,
        product_id INT,
        quantity INT,
        price_per_unit DECIMAL(10, 2),
        FOREIGN KEY (order_id) REFERENCES Orders(order_id), #Nama constraint di generate otomatis
        FOREIGN KEY (product_id) REFERENCES Products(product_id) #Nama constraint di generate otomatis
      );
      ```
      ***Dengan constraint***
      ```
      CREATE TABLE Order_Items (
        order_item_id INT AUTO_INCREMENT PRIMARY KEY,
        order_id INT,
        product_id INT,
        quantity INT,
        price_per_unit DECIMAL(10, 2),
        CONSTRAINT fk_order FOREIGN KEY (order_id) REFERENCES Orders(order_id), #Menambahkan nama constraint
        CONSTRAINT fk_product FOREIGN KEY (product_id) REFERENCES Products(product_id)#Menambahkan nama constraint
      );
      ```
    - karena kita sudah membuat query tanpa menambahkan nama constraint kita perlu drop dulu constraint yang lama
      ```
      -- Drop constraint yg lama
      ALTER TABLE Order_Items
      DROP FOREIGN KEY Order_Items_ibfk_1, 
      DROP FOREIGN KEY Order_Items_ibfk_2;

      -- Tambahkan constraint yg baru
      ALTER TABLE Order_Items
      ADD CONSTRAINT fk_order FOREIGN KEY (order_id) REFERENCES Orders(order_id),
      ADD CONSTRAINT fk_product FOREIGN KEY (product_id) REFERENCES Products(product_id);
      ```
      ![Screenshot from 2023-08-23 01-09-46](https://github.com/agilsaputra/Ingest_data_dan_querySQL/assets/22126819/d0a20828-f213-403e-8bc2-c01c6a041456)

      - Sekarang nama constraint dari tabel ```Order_Items``` ▶️ ```Orders``` yaitu ```fk_order``` dan  
 ```Order_Items``` ▶️ ```Products``` yaitu ```fk_product```
      - Nama ini akan mempermudah untuk schema database dan query yang kompleks.



#### 🔑 Control user access dan role 

- buat user baru di database
  ![Screenshot from 2023-08-22 01-24-41](https://github.com/agilsaputra/Ingest_data_dan_querySQL/assets/22126819/331e6bcc-0f16-48bb-9a79-a54179e865ce)
- query membuat user baru
  ```
  CREATE USER 'username' IDENTIFIED BY 'password';
  ```
- setelah itu kita buat role untuk data analyst yaitu user hanya bisa melakukan query SELECT yang berarti user hanya bisa menganalisa data tidak dapat melakukan update dan delete table maupun database
  ```
  mysql> CREATE ROLE DataAnalystRole;
  Query OK, 0 rows affected (0,02 sec)

  mysql> GRANT DataAnalystRole TO 'DataAnalyst'@'%';
  Query OK, 0 rows affected (0,01 sec)

  mysql> GRANT SELECT ON DB_relasi.* TO DataAnalystRole;
  Query OK, 0 rows affected (0,02 sec)

  mysql> SHOW GRANTS FOR 'DataAnalystRole';
  +--------------------------------------------------------+
  | Grants for DataAnalystRole@%                           |
  +--------------------------------------------------------+
  | GRANT USAGE ON *.* TO `DataAnalystRole`@`%`            |
  | GRANT SELECT ON `DB_relasi`.* TO `DataAnalystRole`@`%` |
  +--------------------------------------------------------+
  2 rows in set (0,00 sec)

  ```
- break down query
     - membuat role user ``` CREATE ROLE Nama_Role_User_Bebas; ```
     - menambahkan role yg kita buat ke dalam user ```GRANT Nama_Role_User_Bebas TO 'User_kalian'@'host_kalian';```   
       **note:** ```Nama_Role_User_Bebas``` adalah role yg  kalian buat sebelumnya
     - tambahkan query SELECT yang berarti user hanya bisa menganalisa data tidak dapat melakukan update dan delete table maupun database. Untuk setting privilige bisa [kesini](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html) ```GRANT SELECT ON Database_kalian.* TO Nama_Role_User_Bebas;```   
       **note**: ```Nama_Role_User_Bebas``` adalah role yg  kalian buat sebelumnya    
                 ```*``` adalah memilih semua tabel di database jika kalian ingin spesifik maka ``` Database_kalian.Nama_tabel```
        
  
