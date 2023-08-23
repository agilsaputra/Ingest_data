### 🔌 Relasi Database Mysql dan Control User access dan role 📤 📥

  - melihat koneksi database yaitu username, nama database, hostname, port. Silahkan masuk ke terminal menggunakan user root
    ```
    sudo mysql -u root
    ```
  - lalu masukan password user linux kalian (saya menggunakan linux mint)
  - untuk melihat database silahkan ketikan query berikut
    ```
    SHOW DATABASES;
    ```
    Akan muncul seperti ini
    ```
    mysql> SHOW DATABASES;
    +----------------------+
    | Database             |
    +----------------------+
    | DB_migrasi_1         |
    | DB_migrasi_2         |
    | DB_relasi            |
    | DB_res               |
    | coba                 |
    | information_schema   |
    | ingest_data_terminal |
    | mysql                |
    | performance_schema   |
    | sys                  |
    | test                 |
    | wordpress            |
    +----------------------+
    12 rows in set (0,00 sec)
    ```
    - Selanjutnya untuk melihat semua user database yaitu jalankan query berikut ;
      ```    
      SELECT user, host FROM mysql.user;
      ```
      Akan muncul seperti ini
      ```
      +------------------+-----------+
      | user             | host      |
      +------------------+-----------+
      | DataAnalyst      | %         |
      | DataAnalystRole  | %         |
      | sqluser          | %         |
      | admin            | localhost |
      | admin1           | localhost |
      | debian-sys-maint | localhost |
      | mysql.infoschema | localhost |
      | mysql.session    | localhost |
      | mysql.sys        | localhost |
      | root             | localhost |
      +------------------+-----------+
      10 rows in set (0,00 sec)
      ```
    - atau kalian bisa buat user baru
      ```
      CREATE USER 'nama_user'@'nama_host' IDENTIFIED BY 'password';
      ```
    - Untuk melihat host server kalian ;
      ```
      SHOW VARIABLES LIKE 'hostname';
      ```
      Hasilnya
      ```
      mysql> show variables like 'hostname';
      +---------------+-----------------------+
      | Variable_name | Value                 |
      +---------------+-----------------------+
      | hostname      | gandalf-ThinkPad-T460 |
      +---------------+-----------------------+
      ```
    - Selanjutnya kita bisa cek port server dengan berikut ;
      ```
      SHOW VARIABLES LIKE 'port'; 
      ```
      hasilnya
      ```
      mysql> show variables like 'port';
      +---------------+-------+
      | Variable_name | Value |
      +---------------+-------+
      | port          | 3306  |
      +---------------+-------+
      1 row in set (0,01 sec)
      ```
    - Kita sudah mendapatkan nama database, username, host, dan port.
    - Misalnya kita akan menngunakan database DB_relasi
      ```
      NAMA DATABASE = DB_relasi
      HOSTNAME      = gandalf-ThinkPad-T460
      USER          = admin1
      PASSWORD      = password_user_kalian
      PORT          = 3306
      ```
