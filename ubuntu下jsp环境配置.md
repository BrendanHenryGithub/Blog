# ubuntu下jsp环境配置
>[参考资料](https://my.oschina.net/hao7234/blog/276887)

## 1. 安装java、tomcat7、 mysql

## 2. 配置mysql与java的连接接口
>[接口程序下载](https://dev.mysql.com/downloads/connector/j/)

## 3. jsp文件中调用mysql的语句：

        String url="jdbc:mysql://localhost/Book?user=root&password=Pass4word";

## 4. 开启mysql服务、tomcat7服务：

        service mysql start
        service tomcat7 start

## 5. mysql、tomcat7服务开机启动以及取消命令：

        sudo systemctl disable tomcat7
        sudo systemctl enable tomcat7

## 6. eclipse java EE 编辑器安装及配置：
>[参考资料](http://blog.csdn.net/htttw/article/details/7596232)
