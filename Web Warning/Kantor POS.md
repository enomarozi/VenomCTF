<h1><b>Kantor POS</h1></b>
<pre>
Kantor POS
</pre>
</b><h3>Solution</h3></b>
<p>inspect element Web page disana terdapat komentar</p>
<pre>
<!--username : password | password : username -->
</pre>
<p>Dan, sesuai judul challenge Kantor POS, ini terkait dengan requsts POST. Lakukan requests POST username dan password</p>

```python
>>> import requests
>>> URL = 'http://localhost/CTF/Web_warning/Web-Warning-13.php'
>>> data = {'username':'password','password':'username'}
>>> res = requests.post(URL,data=data).text
>>> res
'<!DOCTYPE html>\n<html>\n<head>\n\t<title>Web Warning-13</title>\n\t<link rel="stylesheet" type="text/css" href="most_template.css" media="all" />\n</head>\n<body align=\'center\' >\n<h3>Mau kirim cepat?, kirim lewat post aja. dijamin OK</h3>Flag is VenomCTF{K1r1m_l3w4t_POST_4j4}<!--username : password | password : username -->\n</body>\n</html>\n'
>>> 
```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{K1r1m_l3w4t_POST_4j4}
</pre>
