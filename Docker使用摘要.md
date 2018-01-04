# Docker使用摘要
>[参考文档](https://docs.docker.com/)
>[镜像加速](https://yeasy.gitbooks.io/docker_practice/content/install/mirror.html)

## Docker安装
1. 使用官方脚本自动安装：
        
        $ curl -fsSL get.docker.com -o get-docker.sh
        $ sudo sh get-docker.sh --mirror Aliyun

2. 将用户加入docker组：（避免使用sudo）

        sudo usermod -aG docker $USER  //需要注销后才能生效

## Dockerfile文件
>[编写示例](https://docs.docker.com/get-started/part2/#dockerfile)

1. 主要语句：

        # Use an official Python runtime as a parent image
        FROM python:2.7-slim

        # Set the working directory to /app
        WORKDIR /app

        # Copy the current directory contents into the container at /app
        ADD . /app

        # Install any needed packages specified in requirements.txt
        RUN pip install --trusted-host pypi.python.org -r requirements.txt

        # Make port 80 available to the world outside this container
        EXPOSE 80

        # Define environment variable
        ENV NAME World

        # Run app.py when the container launches
        CMD ["python", "app.py"]

2. Build the app:

        docker build -t friendlyhello .   //创建一个docker应用
        docker images                     //查看docker镜像

3. 运行编写的镜像：

        docker run -p 4000:80 friendlyhello  // -d 选项表示后台运行 -p 选项指定端口映射
        docker container ls                  // 查看运行的镜像
        docker container stop 1fa4ab2cf395   // 停止指定镜像


## Docker Cloud
1. 注册Docker ID : https://cloud.docker.com/
2. 创建一个个人仓库
3. 将本地编写的镜像push到云端：

        docker login                                    //登录个人账号
        docker tag image username/repository:tag        //选择要上传的本地的镜像
        docker push username/repository:tag             //上传镜像
        docker run -p 4000:80 username/repository:tag   //在其他机器上运行该镜像，docker会自动拉取镜像文件