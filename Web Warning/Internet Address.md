<h1><b>Internet Address</h1></b>
<pre>
Internet Address
</pre>
</b><h3>Solution</h3></b>
<p>IP kita tidak diizinkan untuk mengakses URL, disini terkait dengan header <b>X-Forwarded-For</b></p>
<p>Ganti IP address dengan parameter X-Forwarded-For</p>

```console
root@Python:/home/venom/Downloads# curl --header "X-Forwarded-For:127.0.0.1" http://localhost/CTF/Web_warning/Web-Warning-10.php
<!DOCTYPE html>
<html>
<head>
	<title>Web Warning-10</title>
	<link rel="stylesheet" type="text/css" href="most_template.css" media="all" />
</head>
<body align='center'>
<h3 class='success'>OK your ip is 127.0.0.1, Flag is VenomCTF{S3rv3r_r3quest_addr355}

</body>

```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{S3rv3r_r3quest_addr355}
</pre>
