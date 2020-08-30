<h1><b>Bug Comparison</h1></b>
<pre>
Bug Comparison
</pre>
</b><h3>Solution</h3></b>
<p>Pada challenge ini kita diberikan source sebagai clue</p>

```php
$username = $_GET['username'];
$password = $_GET['password'];
$real_password = md5("venom19183419");
if (($password==$real_password && $password !== $real_password)|| ($real_password == $password &&  $real_password !== $password))
{
	if (strlen($password)==strlen($real_password) && $username == "admin")
	{
		echo "Flag";
	}
	else
	{
		echo "Failed";
	}
}
else
{
	echo "Failed";
}
```
<p>Pada source terdapat 2 statment checking input username dan password, disana juga dipastikan bahwa username yaitu <b>admin</b>, yang perlu harus diperhatikan pada 
challenge ini yaitu perbedaan "==" dengan "===" atau "!=" dengan "!=="</p>
<pre>
"==" dan "!=" yaitu me-check kondisi yang isinya sama, tanpa memperhatikan type data
"===" dan "!==" yaitu me-check kondisi yang isinya dengan type datanya
</pre>
<p>Pada cheking pertama yaitu isi $password dan $real_password harus bernilai sama(True), dan isi sama type data $real_pass tidak sama $password</p> 
<p>Untuk bypass form dan logika statment dengan menginput username=admin dan list password yang dapat digunakan</p>
<pre>
0e103599092511323593267831730970
0e103599092511323593267831730971
0e103599092511323593267831730972
0e103599092511323593267831730973
0e103599092511323593267831730974
0e103599092511323593267831730975
0e103599092511323593267831730976
0e103599092511323593267831730978
0e103599092511323593267831730979
00000000000000000000000000000000
</pre>
<p>Dan MD5hash venom19183419 = 0e103599092511323593267831730977 sehingga tidak menghasilkan nilai True pada statment !==, Jadi angka terakhir harus dimodif dengan 1 byte angka yang lain, dan penjelasan lainnya lanjut dibawah</p>

```php
echo ($password == $real_password);echo "</br>"; #True
echo ($password !== $real_password);echo "</br>"; #True
echo (($password == $real_password && $password !== $real_password)); #True
```
<p>Selanjutnya Logika dibalik operasi OR, yaitu kebalikan dari operasi sebelumnya</p>

```php
echo ($real_password == $password);echo "</br>"; #True
echo ($real_password !== $password);echo "</br>"; #True
echo (($real_password == $password && $real_password !== $password)); #True
```
<p>Ingat, tanda !== akan menjuggling type string dari <b>md5("venom19183419") = 0e103599092511323593267831730977</b> menjadi integer, sehingga 0e103599092511323593267831730977 dibaca menjadi 0 exponent 103599092511323593267831730977 atau 0**103599092511323593267831730977, e dilambangkan dengan exponent sehingga hasil (0**103599092511323593267831730977)=0</p>

<p align='justify'>Sehingga logika ((1 AND 1) OR (1 AND 1)) = 1, dan lanjut ke statment ke-2 yaitu terdapat fungsi strlen() untuk variabel $password yang menentukan panjang password harus sama dengan strlen() variabel $real_password. Diketahui panjang hash MD5=32, berarti panjang $password harus 32 supaya bernilai 1(True) dan username harus <b>admin</b>, sehingga logikanya ((1 AND 1) AND 1) = 1. Sehingga muncul pesan dan flag didapatkan</p>
<pre align='center'>
Congrast, your flag is VenomCTF{c0mpar1son_equal_4nd_1d3ntic}
</pre>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{c0mpar1son_equal_4nd_1d3ntic}
</pre>
