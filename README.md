TODO
Part 2
Ben Personal Page

Part 3
STEP 4 - README
---

# STEP 6
Install and Active `mod_security`

``` bash
sudo apt update
sudo apt install libapache2-mod-security2 -y
```

Adding config to `/etc/apache2/mods-available/security2.conf`

``` bash
<IfModule mod_security2.c>
    SecRuleEngine On
    SecServerSignature "CSE135 Server"
</IfModule>
```

Reload appache
``` bash
sudo a2enmod security2
sudo systemctl restart apache2
```

Check the result
``` bash
curl -I https://yourdoman.site
# output

# HTTP/1.1 401 Unauthorized
# Date: Tue, 11 Aug 2026 01:22:41 GMT
# Server: CSE135 Server
# WWW-Authenticate: Basic realm="Restricted Content"
# Content-Type: text/html; charset=iso-8859-1

```
---

STEP 8 - README + GoAccess setup
