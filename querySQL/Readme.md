## Beberapa contoh query di mysql

- tabel yang di gunakan untuk query yaitu ini [tabel database](https://github.com/agilsaputra/Ingest_data_dan_querySQL/tree/master/querySQL/data%20classing%20rock%20song)

  #### Query untuk menampilkan artis yang mempunyai lagu paling banyak
- query untuk menampikan artis yang mempunyai lagu paling banyak
 ```
  SELECT `ARTIST CLEAN` AS ARTIS,                 # Memilih tabel artis_clean dengan alias ARTIS
	 COUNT(`ARTIST CLEAN`) AS TOTAL_LAGU     # Menghitung artis_clean dengan alias TOTAL_LAGU
  FROM test_table tt 
  GROUP BY `ARTIST CLEAN` 
  ORDER BY TOTAL_LAGU DESC ;                      # Mengurutkan Berdasarkan alias TOTAL_LAGU secara descending 

 ```
- result dari query diatas [hasil top query top song](https://github.com/agilsaputra/Ingest_data_dan_querySQL/blob/master/querySQL/1.%20output%20query%20query%20artis%20yang%20mempunyai%20lagu%20yang%20paling%20banyak.csv)

  #### Query untuk menampilkan lagu berdasarkan tahun
  - Query dibawah menggunakan nested query atau sub query dengan mengitung ```Release Year``` berdasarkan tahun yg di pilih dan mengurutkan dr paling atas
  ```
  SELECT
  `Artist Name`,
    MAX(`1970`) AS `1970`,
    MAX(`1971`) AS `1971`,
    MAX(`1972`) AS `1972`,
    MAX(`1973`) AS `1973`,
    MAX(`1974`) AS `1974`,
    MAX(`1975`) AS `1975`
  FROM (
    SELECT
      `ARTIST CLEAN` AS `Artist Name`,
      SUM(CASE WHEN `Release Year` = 1970 THEN 1 ELSE 0 END) AS `1970`,
      SUM(CASE WHEN `Release Year` = 1971 THEN 1 ELSE 0 END) AS `1971`,
      SUM(CASE WHEN `Release Year` = 1972 THEN 1 ELSE 0 END) AS `1972`,
      SUM(CASE WHEN `Release Year` = 1973 THEN 1 ELSE 0 END) AS `1973`,
      SUM(CASE WHEN `Release Year` = 1974 THEN 1 ELSE 0 END) AS `1974`,
      SUM(CASE WHEN `Release Year` = 1975 THEN 1 ELSE 0 END) AS `1975`
  FROM
    test_table 
  GROUP BY
    `ARTIST CLEAN`
  ) AS subquery
  GROUP BY
    `Artist Name`
  ORDER BY
    MAX(`1970`) DESC,
    MAX(`1971`) DESC,
    MAX(`1972`) DESC,
    MAX(`1973`) DESC,
    MAX(`1974`) DESC,
    MAX(`1975`) DESC;

- hasil dari query tersebut yaitu [hasil query](https://github.com/agilsaputra/Ingest_data_dan_querySQL/blob/master/querySQL/2.%20output%20query%20query%20top%20artis%20berdasarkan%20tahun.csv)








