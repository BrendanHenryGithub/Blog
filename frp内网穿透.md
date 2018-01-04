# frp内网穿透
>[github项目介绍页](https://github.com/BrendanHenryGithub/frp/blob/master/README.md)

## 使用frp实现远程桌面管理内网穿透

1. 在阿里云服务器上安装frp，修改frps.ini如下：

        [common]
        bind_port = 7000  # 阿里云主机需打开7000端口用于frp进行隧道建立

2. 在内网目标主机上安装frp，修改frpc.ini如下：

        [common]
        server_addr = x.x.x.x   # 阿里云主机ip地址
        server_port = 7000   # 指定与阿里云主机的7000端口建立frp隧道

        [ssh]
        type = tcp
        local_ip = 127.0.0.1
        local_port = 3389    # 指定3389端口通信，即远程桌面要使用的端口
        remote_port = 6000      # 指定将本地端口绑定到阿里云的6000端口，需要提前开启阿里云的6000端口

3. 分别在两边运行frp程序

        ./frpc -c ./frpc.ini

4. 现在便可以在任何电脑进行远程桌面访问内网主机

        x.x.x.x：6000   #阿里云主机的6000端口，即在frpc.ini上设置的remote_port.