### 🔖 Relasi Database Mysql dan Access control 👥 🧑‍💻

#### 📊 Relasi database
- Relasi database ini menggunakan database [ini](https://github.com/agilsaputra/Ingest_data_dan_querySQL/blob/master/Relational_Database_dan_AccessControl/DB_relasi.sql)
- Schema tabel dapat dilihat berikut
  <img src="https://github.com/agilsaputra/Ingest_data_dan_querySQL/blob/master/Relational_Database_dan_AccessControl/tabel%20relasi.png" />

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
