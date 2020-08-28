<h1><b>Weak Registration</h1></b>
<pre>
Form Login (Username & Password)
Form Registration (Username & Password)
</pre>
</b><h3>Solution</h3></b>
<p>Coba login dengan username=<b>admin</b> dan password=<b>admin</b> maka muncul pesan</p> 
<pre align='center'>
<b>Your username and password not found, please go to registration form</b>
</pre>
<p>Selanjutnya mencoba registrasi dengan username=<b>Eno</b> password=<b>Asalan</b> dan registrasi success, dan mencoba login maka muncul pesan</p>
<pre align='center'>
<b>Your success eno, but your not admin</b>
</pre>
<p>Jadi, kita diminta untuk Login sebagai admin, mari kita coba registrasi dengan username=<b>admin</b>, maka muncul pesan</p>
<pre align='center'>
<b>Your username is already registered</b>
</pre>
<p>Dan ternyata username sudah terdaftar, mari kita coba registrasi dengan username=<b><<space>space>admin</b> ditambah space di depan, dan coba login. maka berhasil dan flag didapatkan</p>
<pre align='center'>
<b>Success, i trust your is admin, Flag is VenomCTF{adm1n_is_pow3fulll}</b>
</pre>
<p>Kelemahan login form terdapat pada fungsi php yang selalu melakukan pemeriksaan username dengan fungsi strpos(), fungsi strpos() selalu bernilai True jika sebuah substring terdapat didalam sebuah string, contohnya seperti dibawah ini</p>

```php
<?php
$real_username = "admin";
$fake_username = " admin";
$result = strpos($fake_username, $real_username);
echo $result;
?>
```
<p>Hasil program</p>
<pre>
1
</pre>
<p>Hasil bernilai 1 karena string <b>admin</b> terdapat pada <b><<space>space>admin</b> pada byte 1 </p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{adm1n_is_pow3fulll}
</pre>
