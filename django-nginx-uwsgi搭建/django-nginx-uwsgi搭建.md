# django-nginx-uwsgi 搭建

>[参考资料1](http://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html)
>[参考资料2](https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-uwsgi-and-nginx-on-ubuntu-16-04#install-and-configure-nginx-as-a-reverse-proxy)

## 主要命令

1. systemctl start nginx uwsgi (启动服务)
2. systemctl enable nginx uwsgi (开机启动配置命令)
3. tail -F /var/log/nginx/error.log (查看nginx的错误日志)
4. systemctl daemon-reload (更新服务项配置)

## 主要步骤

1. 依次创建好:_nginx.conf _uwsgi.ini uwsgi.service三个文件
2. 使用ln -s 命令分别将上述三个文件链接至相应位置(ln命令必须用完整路径):
    _nginx.conf -> /etc/nginx/sites-enabled/
    _uwsgi.ini -> /etc/uwsgi/sites/
    _uwsgi.service -> /etc/systemd/system/
3. 设置django项目中的settings.py中的HOST及STATIC路径:
    ALLOWED_HOSTS = ['your_server_domain_or_IP', 'second_domain_or_IP', . . .] STATIC_ROOT = os.path.join(BASE_DIR, "static/")
4. 设置好STATIC路径后运行: ./manage.py collectstatic

## 注意事项

1. uwsgi最好是用全局pip安装而不是virtualenv中的pip安装
2. 用非root用户创建即可,不需要其他用户(创建普通用户的命令useradd)