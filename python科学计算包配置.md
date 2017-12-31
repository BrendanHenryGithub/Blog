# python科学计算套件配置

## 1。pythn库安装
1.1 linux下直接运行：
        
        pip install numpy scipy matplotlib jupyter

1.2 windows下需要先安装python
        
        安装完后先运行：pip install wheel jupyter
        在去：http://www.lfd.uci.edu/~gohlke/pythonlibs/ 下载对应python版本的numpy+mkl和scipy库
        注意下载完后可能要手动修改文件后缀为.whl ，不然无法安装
        然后运行：pip install scipy*.whl
        最后在安装numpy：pip install numpy*.whl

## 2. pip下载时速度慢需要配置国内的阿里源
2.1 linux下在 ~/.pip 下建立pip.conf文件，并添加如下内容：

        [global]
        trusted-host=mirrors.aliyun.com
        index-url=http://mirrors.aliyun.com/pypi/simple/

        或者手动启用指定源：
        pip install --trusted-host=mirrors.aliyun.com -i http://mirrors.aliyun.com/pypi/simple/

2.2 windows下在 %HOMEPATH% 下建立pip 文件夹，在里面建立pip.ini 文件，并添加如下内容：

        [global]
        trusted-host=mirrors.aliyun.com
        index-url=http://mirrors.aliyun.com/pypi/simple/

3. vscode编辑器安装jupyter插件
jupyter 插件使用时在文档开头添加： #%% 便可出现 RUN 按钮运行jupyter

