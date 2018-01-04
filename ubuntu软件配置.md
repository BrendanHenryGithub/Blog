# Ubuntu软件配置

## 0. 安装chrome
0. 准备好离线安装包。sudo dpkg -i goo*
1. 修复依赖包。sudo apt-get -f install

## 1. xx-net配置
>[github手册](https://github.com/XX-net/XX-Net/wiki/How-to-use)
0. linux下开启ipv6代理或者隧道代理：
    - sudo apt-get install miredo
    - sudo miredo -f 
1. ubuntu 下安装:
    -  sudo apt-get install libffi-dev
    -  sudo apt-get install python-openssl
    -  sudo apt-get install python-gtk2
    -  sudo apt-get install python-appindicator
    -  sudo apt-get install libnss3-tools
2. 启动命令：
    - 命令行下运行./start
3. 配置chrome插件:
4. 配置appid: maroonjohn-1257|maroonjohn-1258|maroonjohn-1259

## 2. 安装有道词典
0. 下载dpkg安装包
1. 手动去除安装包里的无效依赖[csdn资料](http://www.cnblogs.com/scplee/p/5489024.html)

## 3. 安装搜狗拼音
0. 下载dpkg安装包
1. dpkg安装，apt修复。
2. 进入系统设置>语言支持。更新语言配置包
3. 注销后重新进入配置里加上sougoupinyin

## 4. 安装zathura
>[网络文档](http://archive.3zso.com/archives/zathura-pdf-reader.html)
0. 直接apt安装即可

## 5. 安装python虚拟环境
>[官方手册](https://virtualenv.pypa.io/en/stable/)
0. 先apt安装Python-pip3
1. pip3 install virtualenv
2. 创建一个与系统独立的py35环境
    - mkdir py35env
    - virtualenv -p /usr/bin/python3 py35env
    - source ./py35env/source/bin/activate  //在同一命令行再运行code，即可将vscode的python环境自动设置为虚拟环境
3. 一般情况下在独立环境使用python是更方便的能避免与系统依赖冲突。

## 6. 安装vscode
0. dpkg安装apt修复
1. 界面定制 One Dark Pro，VSCode Great Icons
2. 常用组件：
    - c/c++
    - Python  //会提示安装pylint
    - Jupyter //需pip配合安装 jupyter、numpy、scipy、matplotlib
    - Live Server //可局域网访问
    - HTML Snippets

## 7. 安装vim
0. apt安装即可
