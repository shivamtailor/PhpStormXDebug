## :beetle: Install and Configure xDebug on MacOS for PhpStorm :elephant:

:warning: This guide only applies to [Homebrew](https://brew.sh/2018/04/09/homebrew-1.6.0/) v1.6+
* Check your version `brew --version` before proceeding

* Assuming that you have already installed php and apache via [Homebrew](https://brew.sh/) v1.6+
* **Install [xDebug](https://xdebug.org/docs/install) php extension**
```
pecl channel-update pecl.php.net
pecl clear-cache

# If you have php v5.6
pecl install xdebug-2.5.5
# If you have php v7.x
pecl install xdebug

pecl clear-cache
```

* **Edit your `ext-xdebug.ini`** 
* Your `ext-xdebug.ini` file path should look like this (depends on php version installed)
    - `/usr/local/etc/php/7.1/conf.d/ext-xdebug.ini`
* Add these lines by overwriting exiting 
```
;zend_extension="/usr/local/Cellar/php@7.1/7.1.21/pecl/20160303/xdebug.so"
zend_extension="xdebug.so"
xdebug.remote_enable = 1
xdebug.remote_port = 9000
xdebug.idekey = PHPSTORM
xdebug.show_error_trace = 1
xdebug.remote_autostart = 0
xdebug.file_link_format = phpstorm://open?%f:%l
```

* **Update your `php.ini`** 
* When installing xdebug extension using `pecl`, it also updates our `php.ini` file, but we don't need that.
* Find your `php.ini` file, file path should look like this (depends on php version installed)
    - `/usr/local/etc/php/7.1/php.ini`
* Remove any occurrence of `zend_extension="xdebug.so"`  from this file

* Restart the apache server to reflect changes
```
sudo apachectl -k restart
```

* **Configure phpStorm**
* Go through - Settings >> Languages & Frameworks >> PHP >> Debug
* Check that 'Debug port' is the same you have in your `ext-xdebug.ini`. In our case it was `9000`.
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
