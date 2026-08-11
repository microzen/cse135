# Login to the site
- Username: grader
- Password: grader

# Deployment (Part 2)
Deployment is fully automated via GitHub Actions which is triggered during every push to main branch. We utilized
appleboy/scp-action to copy files over SSH to our droplet server. This required making a independent "deploy" user on our server with its
own SSH key which it uses to authenticate and pull files from shared repo. Authentication information like private key are stored in GitHub Secrets.

# Login (Part 3: Step 4)
- Username: grader
- Password: grader

# Compression (Part 3: Step 5)
It seems like compression was automatically enabled for our site via mod_deflate (Encoding: gzip). This encoding shrinks the size of the HTML file sent over the web pretty significantly with the tradeoff of requiring more processing to send and unpack this encoded file. Considering how barebones our website is right now though this processing time vs. transfer speed tradeoff is not really noticeable. 

# Obscure Identity (Part 3: Step 6)
Install and Activate `mod_security`

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

TODO:
STEP 8 - README + GoAccess setup

TODO:
Checking List:
- [ ] Names of all members in your team
- [x] The password for user "grader" on your Apache server
- [ ] Summary of changes to HTML file in DevTools after compression
- [ ] Username/password info for logging into the site
- [ ] `github-deploy.mpeg` or `github-deploy.gif` - showing Github deploy process
