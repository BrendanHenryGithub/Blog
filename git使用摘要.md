# git使用摘要
>本摘要采用Markdown语法编写   
>[参考手册](http://gitref.org/zh/remotes/#fetch)

## git命令行常用命令
- git config --global user.name "NAME"  用于git的用户名设置 （必须设置了用户名和邮箱才能进行提交远端服务器的操作）
- git config --global user.email "EMAIL"  用于git的用户邮箱设置 
- git init 初始化一个本地git仓库
- git clone url 克隆指定的仓库
- git add filename 添加文件到缓存
- git status 查看当前缓存内容
- git diff 查看从上次提交以来的改动
- git commit -m '进行注释' 实际存储缓存
- git branch 列出可用分支
- git branch (-d) branchname 创建(删除)新分支
- git checkout branchname 切换到该分支
- git merge branchname 将该分支合并到当前分支 (如果有合并冲突了需要手工处理,再执行git add)
- git log --online --graph 查看历史中什么时候出现了分支、合并。
- git remote 列出远端别名
- git remote add [alias] [url] 为项目添加一个远端仓库
- git remote rm [alias] 删除一个远端仓库
- git fetch [alias] 从远端下载更新,需要手动合并
- git pull [alias] 与远端同步,会自动合并
- git push [alias] [branchname] 推送你的新分支到远端仓库
- git push -u [alias] [master] 初始化本地库,自动建立与远端库的跟踪
- git log [网络资源](http://gitref.org/zh/inspect/#log)
- git diff [网络资源](http://gitref.org/zh/inspect/#log)

## github远端操作
>通过命令行来创建github远端库的方法参见[网络资源](https://my.oschina.net/eduOSS/blog/287824)

- source ~/.bash_profile
- github-create [repo name]
