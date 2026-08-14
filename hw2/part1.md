1. Download perl code to `/var/www/html`
2. Install mod_perl
3. install Json library for perl
4. Set up config
5. Restart server

# Install and restart

``` bash
sudo apt update
sudo apt install -y libapache2-mod-perl2 libjson-perl
sudo a2enmod perl
sudo apachectl configtest
sudo systemctl restart apache2
```

# Config
``` config
Alias /perl/ /var/www/html/cgi-bin/
<Directory /var/www/html/cgi-bin/>
    Options +ExecCGI
    SetHandler perl-script
    PerlResponseHandler ModPerl::Registry

    PerlOptions +ParseHeaders
    PerlOptions +GlobalRequest

    Require all granted
</Directory>
```