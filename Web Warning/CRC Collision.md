<h1><b>CRC Collision</h1></b>
<pre>
CRC Collision
</pre>
</b><h3>Solution</h3></b>
<p>Pada web-page terdapat 2 clue</p>
<p>Clue Ke-1</p>
<pre>
Bisakah kamu temukan flag, tadi saya mendapatkan clue bahwa flag terkait dengan desimal value 3435 dari text string
</pre>
Clue Ke-2

```php
$crc = 0xffff;
for($i=0;$i<strlen($userid);$i++)
{
    $x = (($crc >> 8) ^ ord($userid[$i])) & 0xff;
    $x ^= $x >> 4;
    $crc = (($crc << 8) ^ ($x << 12) ^ ($x << 5) ^ $x) & 0xffff;
    $crc %= 0xfff;
}
```
<p>Judulnya terkait dengan CRC Collision, dan disini kita diminta untuk login dengan value stringnya = 3435. Pada source PHP itu untuk generate string value, lakukan bruteforce 
untuk generate string</p>

```python
import itertools
from string import ascii_lowercase

username = itertools.product(ascii_lowercase,repeat=5)

def bruteforce(user):
    crc = 0xffff
    for i in range(len(user)):
        x = ((crc >> 8) ^ ord(user[i])) & 0xff
        x ^= x >> 4
        crc = ((crc << 8) ^ (x << 12) ^ (x << 5) ^ x) & 0xffff
        crc %= 0xfff
    if crc == 3435:
        print(user,crc)
for i in username:
    bruteforce(''.join(i))
```
<p>Hasil Program</p>
<pre>
aafaf 3435
aafig 3435
aanho 3435
aatch 3435
aatki 3435
abfgl 3435
abfom 3435
abnfd 3435
abnne 3435
abtej 3435
abtmk 3435
acfeb 3435
acfmc 3435
acndj 3435
</pre>
<p>Edit Cookie dengan beberapa username yang sudah didapat dan reload page maka muncul pesan berisi flag</p>
<pre>
Congrast, Your flag is VenomCTF{Ex4mpl3_crc_c0llis1on}
</pre>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{Ex4mpl3_crc_c0llis1on}
</pre>
