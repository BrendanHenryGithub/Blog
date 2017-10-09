# LAMP环境搭建
>本总结参考如下博客   
>[Mysql安装](http://blog.csdn.net/cryhelyxx/article/details/49757217)    
>[整体环境安装](http://www.voidcn.com/blog/490617581/article/p-5797501.html)

## Mysql安装注意事项
1. 官网下载Mysql的二进制包(不是.deb包)600+MB;
2. Mysql5.7版本的安装过程与早期版本有区别;
3. Mysql的默认目录结构为:主程序 /usr/local/mysql  数据库 /usr/local/mysql/data/ (注意:安装时若指定其他目录则要修改该目录的权限 chown -R mysql:mysql /usr/local/mysql/data)
4. ubuntu下设置成开机启动时无法使用chkconfig工具(已被update-rc.d)取代,故相应命令改为update-rc.d mysqld defaults
5. 首次登入后会提示修改密码,注意保留好最开始的随机密码.

## php环境(php-FPM+Fastcgi)搭建
>特别注意php-fpm无法跟mod_fcgid结合使用.如果想采用php-FPM加fcgid话可以考虑mod_proxy_fcgid
>有关php环境讲解[参考博客](http://www.awaimai.com/371.html)   
>搭建过程[参考博客](http://weizhifeng.net/php5.3-apache2-fastcgi-php-fpm.html)  

### php的./configure参数
>部分参数中文说明[参考博客](http://camnpr.com/php-python/1774.html)     

		# ./configure \
		--prefix=/usr/local/php \
		--with-apxs2=/usr/local/apache2/bin/apxs \(在使用cgi情况下这条参数不需要,有关apxs的作用参见[参考博客1](http://camnpr.com/php-python/1774.html)[参考博客2](http://blog.51yip.com/apachenginx/871.html))
		--with-config-file-path=/usr/local/php/etc  \(后续步骤中要拷贝配置文件cp php.ini-production /usr/local/php/etc/php.ini)
		--with-mysql=/usr/local/mysql \
		--with-libxml-dir \(libxml默认开启,不需另加,除非安装于非默认目录)
		--with-gd \
		--with-jpeg-dir \
		--with-png-dir \
		--with-freetype-dir \
		--with-iconv-dir \
		--with-zlib-dir \
		--with-bz2 \
		--with-openssl \
		--with-mcrypt \
		--enable-soap \
		--enable-gd-native-ttf \
		--enable-mbstring \
		--enable-sockets \
		--enable-exif \
		--disable-ipv6

>以下为最新一次搭载Laravel框架的编译参数

		./configure \
		--prefix=/usr/local/php \
		--with-config-file-path=/usr/local/php/etc \
		--with-mysql=/usr/local/mysql \
		--enable-bcmath \
		--with-openssl \
		--enable-mbstring \
		--enable-cgi \
		--enable-fpm \
		注:Laravel要求的扩展中tokenizer,PDO高版本默认可用

### php的配置
>先cp /usr/local/src/php-5.6.26/php.ini-development /usr/local/php/etc/php.ini 在对php.ini进行修改
>注意在修改扩展时不需要手动添加已经在编译时加入的扩展,重复配置会导致错误

### php的动态扩展--phpize的使用
>手动添加扩展.[参考博客](http://blog.csdn.net/xifeijian/article/details/22690613)
>注:编译时已经附加的模块不需从新添加,否则会报错.

1. php自带有部分扩展库,所在目录为/usr/local/src/php-5.6.26/ext (php的运行时加载扩展的目录为/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/)
2. 进入要编译的扩展目录先执行/usr/local/php/bin/phpize
3. 再执行编译
			./configure
			--with-php-config=/usr/local/php/bin/php-config
4. 编译到make即可,然后再当前目录的modules目录下复制生成的文件到php运行时的扩展目录即可

## apache2搭建
### apache与php的几种结合方式
模块模式;CGI模式;fastCgi模式，apche内置进程管理器;fastCgi模式，php-fpm进程管理器
### apache安装
>以下为最新一次搭载Laravel框架的编译参数

		./configure
		--prefix=/usr/local/apache2 \
		--enable-so \
		--enable-rewrite

>以下为mod_fcgid的安装
>最新一次安装时发现无法采用mod_fcgid与php-fpm的组合方案,故改用了mod_fcgid加apache的任务管理

		APXS=/usr/local/apache2/bin/apxs ./configure.axps(执行这条命令最开始报错后安装了apache2-dev后可以执行)
		make
		make install
		(注意安装完后需在modules/fcgid/.libs中拷贝mod_fcgid.so至apache的modules目录下)

>http.conf的配置添加如下代码即可

			LoadModule fcgid_module modules/mod_fcgid.so

			<IfModule mod_fcgid.c>
    			AddHandler fcgid-script .fcgi .php
    			#php.ini的存放目录
    			FcgidInitialEnv PHPRC "/usr/local/php/etc"
    			# 设置PHP_FCGI_MAX_REQUESTS大于或等于FcgidMaxRequestsPerProcess，防止php-cgi进程在处理完所有请求前退出
    			FcgidInitialEnv PHP_FCGI_MAX_REQUESTS 1000
    			#php-cgi每个进程的最大请求数
    			FcgidMaxRequestsPerProcess 1000
    			#php-cgi最大的进程数
    			FcgidMaxProcesses 5
    			#最大执行时间
    			FcgidIOTimeout 120
    			FcgidIdleTimeout 120
    			#php-cgi的路径
    			FcgidWrapper "/usr/local/php/bin/php-cgi" .php
    			AddType application/x-httpd-php .php
			</IfModule>

			<Directory "/usr/local/apache2/htdocs">
    			Options Indexes FollowSymLinks ExecCGI
    			Order allow,deny
    			Allow from all
    			AllowOverride All
			</Directory>
