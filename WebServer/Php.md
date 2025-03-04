# [Install PHP](https://www.sitepoint.com/how-to-install-php-on-windows/)

## Download the PHP files
Get the latest [PHP x64 Thread Safe ZIP package](https://windows.php.net/download/).

## Extract the files
Create a new php folder in the root of your `C:\` drive and extract the content of the ZIP into it. You can install PHP anywhere on your system, but you’ll need to change the paths referenced below if you use anything other than `C:\php`.

## Add `C:\php` to the PATH environment variable

![image](https://github.com/user-attachments/assets/1ffbf76d-a70d-4fe6-8d69-a5ff5c7a55bd)


## Configure php.ini
PHP’s configuration file is `php.ini`. This doesn’t exist initially, so copy `C:\php\php.ini-development` to `C:\php\php.ini`. This default configuration provides a development setup which reports all PHP errors and warnings.

You can edit `php.ini` in a text editor, and you may need to **change lines** such as those suggested below (use search to find the setting). In most cases, you’ll need to **remove** a leading semicolon (`;`) to uncomment a value.

First, enable any required extensions according to the libraries you want to use.

```txt
extension=curl
extension=gd
extension=mbstring
extension=pdo_mysql
```

If you want to send emails using PHP’s mail() function, enter the details of an SMTP server in the [mail function] section (your ISP’s settings should be suitable):

```txt
[mail function]
; For Win32 only.
; http://php.net/smtp
SMTP = mail.myisp.com
; http://php.net/smtp-port
smtp_port = 25

; For Win32 only.
; http://php.net/sendmail-from
sendmail_from = my@emailaddress.com
```

## Configure PHP as an Apache module
Ensure Apache is **not running** and open its `C:\Apache24\conf\httpd.conf` configuration file in a text editor. Add the following lines to the bottom of the file to set PHP as an Apache module (change the file locations if necessary but use forward slashes rather than Windows backslashes):

# PHP8 module
```cinfig
PHPIniDir "C:/php"
LoadModule php_module "C:/php/php8apache2_4.dll"
AddType application/x-httpd-php .php
```

Optionally, change the `DirectoryIndex` setting to use index.php as the default in preference to index.html. The initial setting is:

```config
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```

Change it to:

```config
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
```

**Save** `httpd.conf` and test the updates from a cmd command line:

```powershell
cd C:\Apache24\bin
httpd -t
```

`Syntax OK` will appear … unless you have errors in your configuration. If all went well, start Apache with `httpd`.

```powershell
cd C:\Apache24\bin
httpd
```


## Test a PHP file
Create a new file named `index.php` in Apache’s web page root folder at `C:\Apache24\htdocs`. Add the following PHP code:

```php
<?php
phpinfo();
?>
```

