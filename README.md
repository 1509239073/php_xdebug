### php升级 Xdebug升级

**1.下载需要的素材** 
* php版本 [PHP 7.2 (7.2.25)](https://windows.php.net/download#php-7.4
  "7.2.25")
* Xdebug版本 [Xdebug 2.6.0beta1](https://xdebug.org/download "PHP 7.2 VC15 (32 bit)")
 
* 注意php对应的版本和Xdebug 版本千万不要太高，**版本冲突**

**2.更改环境变量** 
* 右击此电脑->属性->高级系统设置->环境变量->系统变量->Path
* 新增新的php.exe 的位置
* win + R 打开 输入`cmd`
* 输入 `php -v` 查看php 版本 
```
PHP 7.2.25 (cli) (built: Nov 20 2019 18:56:00) ( NTS MSVC15 (Visual C++ 2017) x86 )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Xdebug v2.6.0beta1, Copyright (c) 2002-2017, by Derick Rethans
```
**3.开启php.ini扩展**
* 将Xdebug后缀为dll的放在ext文件夹下，重命名为`php_xdebug.dll`
* 打开`php.ini` 配置  zend_extension="***\php-7.2.25-nts\ext\php_xdebug.dll"
```
[XDebug]
xdebug.profiler_output_dir=""
xdebug.trace_output_dir=""
zend_extension="***\php-7.2.25-nts\ext\php_xdebug.dll"
xdebug.remote_port=9100
xdebug.remote_enable=on
xdebug.remote_autostart = on
xdebug.var_display_max_children=8000
xdebug.var_display_max_data=5120000
xdebug.var_display_max_depth=8
```
**4.查看php.ini扩展开启**
* win + R 打开 输入`cmd`
* 输入 `php -` 查看php module 
```
[PHP Modules]
bcmath
calendar
Core
ctype
curl
date
dom
exif
fileinfo
filter
gd
gettext
gmp
hash
iconv
imap
intl
json
ldap
libxml
mbstring
mysqli
mysqlnd
odbc
openssl
pcre
PDO
pdo_mysql
PDO_ODBC
pdo_pgsql
pdo_sqlite
Phar
readline
Reflection
session
SimpleXML
SPL
standard
tokenizer
wddx
xdebug
xml
xmlreader
xmlwriter
zip
zlib

[Zend Modules]
Xdebug
```
* 写个php文件查看phpinfo() 是否开启扩展。


**5.配置phpstorm** 
* Ctrl + Alt + S 打开配置项
* Languages & Frameworks -> PHP -> Debug -> Debug Port 9100
* Languages & Frameworks -> PHP 找到对应php.exe 位置
* Languages & Frameworks -> PHP -> Debug -> DBGP Proxy 配置key IDE
  key可在php.ini里面设置，Host也可自行调整
```
IDE key: Administrator
Host: localhost
Port: 9100
```
* Run -> Edit Configurations
* 网上自行找图 选个PHP Web Application自己玩去


### 踩坑点 
1. 浏览器提供了Xdebug的插件 
2. Languages & Frameworks -> PHP ->Debug -> DBGP Proxy 一定要配置
3. Xdebug版本一定要对应
4. Port 设置 不要冲突即可 ,可以尝试点击`Break at first line in PHP scripts
   option (from Run menu)` 此项可在 Run -> Break at first line in PHP
   scripts 中取消
```
Debug session was finished without being paused
It may be caused by path mappings misconfiguration or not synchronized local and remote projects.
To figure out the problem check path mappings configuration for 'localhost_8080' server at PHP|Servers or enable Break at first line in PHP scripts option (from Run menu).
Do not show again
```

