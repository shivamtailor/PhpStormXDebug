## :beetle: Install and Configure xDebug on Ubuntu for PhpStorm :elephant:

* Assuming that you have already installed php and apache
* **Install [xDebug](https://xdebug.org/docs/install) php extension**
```
# Ubuntu 16.04,18.04 php 7.x
sudo apt-get install php-xdebug

# Ubuntu 14.04, php 5.6 
sudo apt-get install php5-xdebug
```

* **Edit your `xdebug.ini`** 
* Your `xdebug.ini` file path should look like this
    - `/etc/php/7.1/mods-available/xdebug.ini`  
* Add these lines without modifying exiting 
```
xdebug.remote_enable = 1
xdebug.remote_port = 9000
xdebug.idekey = PHPSTORM
xdebug.show_error_trace = 1
xdebug.remote_autostart = 0
xdebug.file_link_format = phpstorm://open?%f:%l
```
* Restart the apache server to reflect changes
```
sudo service apache2 restart
```

* **Configure phpStorm**
* Go through - Settings >> Languages & Frameworks >> PHP >> Debug
* Check that 'Debug port' is the same you have in your `xdebug.ini`. In our case it was `9000`.
* Save and close the Settings Dialog

* **Start debugging**
* Create some [breakpoints](https://www.jetbrains.com/help/phpstorm/breakpoints-2.html) in your project 
* Make sure those breakpoints gets executed when your visit your website in browser.
* Start listener by clicking on the telephone :telephone_receiver: button on top toolbar
* If you can't find telephone button; then go through menus - Run -> Start listening for PHP Debug Connections
* In your browser access your project url like this 
```
http://localdomain.test/?XDEBUG_SESSION_START=1
```
* OR use [bookmarks](https://www.jetbrains.com/phpstorm/marklets/) 
* OR use [chrome extension](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=en) 

* You should see a popup window in PhpStorm , click **Accept** connection 
* Done, enjoy debugging !!!

-----

### Disable xdebug
```
sudo phpdismod xdebug
```
### Enable xdebug back 
```
sudo phpenmod xdebug
```
### Disable xdebug for commandline only 
```
sudo phpdismod -s cli xdebug
```

