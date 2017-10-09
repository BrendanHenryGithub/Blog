# aria2文档

## 0.aria2的安装
1. 从github源下载源文件压缩包
2. 解压源文件包并进行编译安装：     
		cd 源文件文件夹
		make clean
		./configure
		make
		make install
3. 编写默认参数配置文件,存在配置文件时默认会加载该文件参数
		cd 源文件文件夹
		vim aria2.conf
4. 建议将参数配置文件权限修改为600(因为配置文件可能包含代理密码等信息)

## 1.aira2的基本操作
1. 直接从指定网址下载
		$ aria2c "http://host/file.zip"   //-d指定目录 -x10 指定连接数为10
2. 使用代理下载
3. 将待下载文件链接写入文本文件，并按该文件进行下载操作

## 2.aria2的扩展操作
1. aria2为命令行程序可配合WebUI使用，
		在命令行中运行：aria2c --enable-rpc --rpc-listen-all
		同时在浏览器中打开：[WebUI页面](file:///home/john/Downloads/webui-aria2-master/index.html)

## 3.aria2的使用技巧与快捷按键
1. 命令行运行时ctrl+c 可停止操作，如果要继续下载只需在原来命令中加上-c 参数即可

## 4.aria2使用备忘
1. aria2的代理下载暂时还有问题，不清楚是否与xx-net有关
2. aria2在使用默认参数下载普通资源时基本可满速，但在下载百度云、bt文件时还需要特别配置参数
3. aria2的百度云破解限速还有待尝试

## 5.相关参考资料
1. [aria2手册页](https://aria2.github.io/manual/en/html/aria2c.html)
2. [aria2部分参数解释](http://aria2c.com/usage.html)
