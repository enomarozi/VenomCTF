<h1><b>Agent 86</h1></b>
<pre>
Agent 86
</pre>
</b><h3>Solution</h3></b>
<p>Browser kita tidak diizinkan untuk mengakses URL oleh user-agent, yang diizinkan hanyalah browser dengan nama <b>venom</b></p>

```console
root@Python:/var/www/html/CTF# curl -A 'venom' http://localhost/CTF/Web_warning/Web-Warning-4.php
<!DOCTYPE html>
<html>
<head>
	<title>Web Warning-4</title>
</head>
<body>
Your browser is allowing<br>Flag VenomCTF{Venom_1s_th4t_y0or?}
</body>
</html>
```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{Venom_1s_th4t_y0or?}
</pre>
