<h1><b>Headsquare</h1></b>
<pre>
Headsquare
</pre>
</b><h3>Solution</h3></b>
<p>Periksa header requests pada URL</p>

```console
root@Python:/var/www/html/CTF# curl --head http://localhost/CTF/Web_warning/Web-Warning-2.php
HTTP/1.1 200 OK
Date: Sun, 30 Aug 2020 09:17:43 GMT
Server: Apache/2.4.43 (Debian)
Flag: VenomCTF{H34der_php_funct10n}
Content-Type: text/html; charset=UTF-8

```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{H34der_php_funct10n}
</pre>
