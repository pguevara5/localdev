### httpd config
File to roadmap setting up a local development environment

##### Set up local ~/Sites directory and create test index.html
```
mkdir ~/Sites
echo "<html><body><h1>My site works</h1></body></html>" > ~/Sites/index.html
```

##### Enable PHP
Go to this file
```
sudo vim /etc/apache2/httpd.conf
```
and uncomment this line:
```
LoadModule php5_module libexec/apache2/libphp5.so
```
###### For OS X Yosemite ONLY
Uncomment the following lines (line numbers in margin):
```
166 LoadModule userdir_module libexec/apache2/mod_userdir.so
493 Include /private/etc/apache2/extra/httpd-userdir.conf
```
Then open the following file:
```
sudo vim /etc/apache2/extra/httpd-userdir.conf
```
And uncomment the following
```
Include /private/etc/apache2/users/*.conf
```

##### For all systems
Create a <username>.conf file
```
sudo vim /etc/apache2/users/<username>.conf
```
For all systems (except Yosemite)
```
<Directory "/Users/<your short user name>/Sites/">
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny
    Allow from localhost
</Directory>
```
For Yosemite
```
<Directory "/Users/<your short user name>/Sites/">
    AddLanguage en .en
    LanguagePriority en fr de
    ForceLanguagePriority Fallback
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny
    Allow from localhost
     Require all granted
</Directory>
```

##### To restart apache with these settings
```
sudo apachectl restart
```