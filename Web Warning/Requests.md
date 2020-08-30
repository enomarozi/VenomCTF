<h1><b>Requests</h1></b>
<pre>
Requests
</pre>
</b><h3>Solution</h3></b>
<p>Kita diminta melakukan requsts untuk mendapatkan flag, jika kita input pada form akan muncul pesan <b>Minta dengan sopan broo..</b></p>

```python
import requests
import re

URL = 'http://localhost/CTF/Web_warning/Web-Warning-7.php'
data = {'flag':'flag'}
res = requests.post(URL,params=data).text
print(res) #This flag VenomCTF{R3qu3st_G3T_for_Fl4g}

```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{R3qu3st_G3T_for_Fl4g}
</pre>
