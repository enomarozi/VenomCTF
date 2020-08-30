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

```php
$statment_1 = "0e103599092511323593267831730977" == md5("venom19183419");
$statment_2 = "0e103599092511323593267831730977" !== md5("venom19183419");
echo $statment_1; #Bernilai True
echo $statment_2; #Bernilai False
echo $statment_1 && $statment_2; #Bernilai False
```
<p>Selanjutnya Logika dibalik operasi OR, yaitu kebalikan dari operasi sebelumnya</p>
<pre>
$statment_1 = md5("venom19183419") == "0e103599092511323593267831730977";
$statment_2 = md5("venom19183419")!== "0e103599092511323593267831730977";
echo $statment_1;
echo $statment_2;
echo $statment_1 && $statment_2;
</pre>
</b><h3>Flag</h3></b>
<pre>
</pre>
