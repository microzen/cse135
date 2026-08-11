# Homework 1 - 8/10/26
**Client Side Basics, Site and Server Configuration**

## Names
- Benjamin Michael
- Yezhi Wu

## Site Links
- [https://benyezhi.site/](https://benyezhi.site/)
- [https://benyezhi.site/members/ben.html](https://benyezhi.site/members/ben.html)
- [https://benyezhi.site/members/yezhi.html](https://benyezhi.site/members/yezhi.html)
- [https://benyezhi.site/hw1/hello.php](https://benyezhi.site/hw1/hello.php)
- [https://benyezhi.site/hw1/report.html](https://benyezhi.site/hw1/report.html)

## Grader Website Login
- Username: grader
- Password: grader

## Grader Server Login
- Username: grader
- Password: benyezhigrader
- Private SSH Key: *Included in Gradescope submission*

# Part 1: Basic Apache Configuration

## Step 7: Default Page Setup 
[initial-index.jpg](initial-index.jpg)

## Step 9: Simple Webpage Setup 
[modified-index.jpg](modified-index.jpg)

## Step 10: Webpage HTML Validation
[validator-initial.jpg](validator-initial.jpg)

## Step 13: Virtual Host Setup 
[vhosts-verify.jpg](vhosts-verify.jpg)

## Step 14: SSL Setup
[SSL-verify.jpg](SSL-verify.jpg)

# Part 2: Building Out a Simple Website

## Deployment
Deployment is fully automated via GitHub Actions which is triggered during every push to main branch. We utilized
appleboy/scp-action to copy files over SSH to our droplet server. This required making a independent "deploy" user on our server with its
own SSH key which it uses to authenticate and pull files from shared repo. Authentication information like private key are stored in GitHub Secrets.

[Github-Deploy.gif](Github-Deploy.gif)

# Part 3: Configuring Your Web Server

## Step 3: PHP Example Page
[php-verification.jpg](php-verification.jpg)

[https://benyezhi.site/hw1/hello.php](https://benyezhi.site/hw1/hello.php)

## Step 5: Compression
It seems like compression was automatically enabled for our site via mod_deflate (Encoding: gzip). This encoding shrinks the size of the HTML file sent over the web pretty significantly with the tradeoff of requiring more processing for the server to send and client to unpack this encoded file. Considering how barebones our website is right now though this processing time vs. transfer speed tradeoff is not really noticeable. 

[compression-verify.jpg](compression-verify.jpg)

## Step 6: Obscure Identity
Installed and activated `mod_security`

``` bash
sudo apt update
sudo apt install libapache2-mod-security2 -y
```

Added config to `/etc/apache2/mods-available/security2.conf`

``` bash
<IfModule mod_security2.c>
    SecRuleEngine On
    SecServerSignature "CSE135 Server"
</IfModule>
```

Reloaded Apache
``` bash
sudo a2enmod security2
sudo systemctl restart apache2
```

Results:
``` bash
curl -I https://yourdoman.site
# output

# HTTP/1.1 401 Unauthorized
# Date: Tue, 11 Aug 2026 01:22:41 GMT
# Server: CSE135 Server
# WWW-Authenticate: Basic realm="Restricted Content"
# Content-Type: text/html; charset=iso-8859-1

```

[header-verify.jpg](header-verify.jpg)

## Step 7: 404 Configuration
[error-page.jpeg](error-page.jpeg)

## Step 8: Verify Logs
[log-verification.jpg](log-verification.jpg)

[report-verification.jpg](report-verification.jpg)

[https://benyezhi.site/hw1/report.html](https://benyezhi.site/hw1/report.html)
