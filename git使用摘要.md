# git 使用摘要
- 参考资料
    - [Pro Git 2nd简体中文版](https://www.gitbook.com/book/bingohuang/progit2/details)

## git 初始化配置
1. 安装git
    - linux下： sudo apt-get install git
    - windows下： https://www.gitbook.com/book/bingohuang/progit2/details
2. 建议在vscode编辑器下使用git
3. git的配置文件：
    - /etc/gitconfig :系统上所有用户的通用配置，git config --system 命令可以修改此配置文件
    - ~/.gitconfig 或 ~/.config/git/config ： 当前用户的配置文件, git config --global 命令可修改此文件
    - git项目下的 .git/config ： 只用于当前项目的配置文件
4. git用户信息：
    1. 安装完git的第一件事就是设置用户名和邮件地址
        ```
        git config --global user.name "USERNAME"
        git config --global user.email "EMAIL@email.com"
        ```
    2. 后续如需在其他项目里更改可以不带global选项的命令覆盖全局配置
5. 可选配置：
    1. 配置文本编辑器：
        ```
        git config --global core.editor vim
        ```
    2. git别名：
        ```
        git config --global alias.lg 'log --oneline --graph --decorate --all'
        ```
    3. 设置代理：
        ```
        开启：
        git config --global https.proxy http://127.0.0.1:1080
        git config --global https.proxy https://127.0.0.1:1080
        关闭：
        git config --global --unset http.proxy
        git config --global --unset https.proxy
        ```
6. 检查配置：git config --list

## git 基础命令
1. 初始化仓库：
    - git init : 从本地初始化或导入git，如果已有项目文件则需要运行git add * 来开始跟踪项目
    - git clone <URL> ： 从远端仓库克隆一个已有的项目

2. 本地仓库的更新操作：
    - git status ： 检查当前文件状态
        ```
        $	git	status	-s
            M	README               //靠左边的M表示表示该文件修改过并放入了暂存区
            MM	Rakefile             //靠右边的M表示修改了但还未放入暂存区
            A		lib/git.rb       //A表示新添加入暂存区的文件
            M		lib/simplegit.rb
            ??	LICENSE.txt          //??号代表未跟踪
        ```    
    - git add <file> : 跟踪该文件，即将该文件添加到暂存区
    - git rm <file> : 取消对该文件的跟踪并在当前工作目录里删除文件，可以加 -f 强制执行
    - git rm --cached <file> ： 取消对文件的跟踪但将文件保留在当前工作目录里。
    - git commit [-m "message"] : 将暂存区的所有更改提交到本地仓库，后续可以将本地仓库上传至远端仓库
     
3. 本地仓库与远端仓库的交互
    - git remote add <remotename> <url> : 添加一个远端仓库并自定义命名
    - git remote -v : 列出该项目的远端仓库信息
    - git remote show <remotename> : 查看指定远端仓库的详细信息
    - git fetch <remotename> <remotebranch>:<localbranch> ： 从指定远端仓库拉取更新,拉取的更新位于指定的本地分支上，后续可以合并或查看拉取的内容
        ```
        git fetch origin refs/heads/master:refs/remotes/origin/master
        ```
    - git push <remotename> <localbranchname>:<remotebranch> : 将指定本地分支推送至远端仓库并命名为所给定的名称
        ```
        git push origin :test    //通过传输一个空的本地分支来达到清除远端仓库上的test分支的目的
        git push origin --delete <branchname> //删除远端仓库的指定分支
        ```
    - git remote rm <remotename> : 删除该远端仓库

4. git的撤销操作
    1. 撤销最近一次的提交，对最近一次提交进行覆盖
        ```
        $ git commit --amend
        //这个命令会将暂存区中的文件提交。	如果自上次提交以来你还未做任何修改(例如,在上次提交后马上执行了此命令),那么快照会保持不变,而你所修改的只是提交信息。
        ```
    2. 从暂存区内撤销文件
        1. 不希望仍保留在当前工作目录：git rm -f <file>
        2. 希望仍保留在工作目录：
            ```
            git rm --cached <file>或者：
            git reset HEAD <file> //推荐使用后者
            ```
    3. 利用之前暂存区的文件来还原当前工作目录下的文件
        ```
        git checkout <file>  //该命令会用暂存区的文件覆盖工作目录的文件，如果同时仍需保留工作目录的修改则需新建分支
        ```
    4. 利用最近的提交历史来还原单独的文件
        ```
        git checkout <file>   //该命令与上一条相同，执行时会先匹配上一种情况，即要实现该目标可能需要先执行reset
        git reset <file>      //该命令将文件从暂存区内移出
        ```
    5. 回退到指定提交节点
        1. 将当前分支回退到指定节点：git reset --hard <commitID>
            ```
            在git pull操作中发生冲突，想撤销可以：git reset --hard //默认回到HEAD节点此处即是pull操作前的节点
            如果直接快速合并了，想撤销可以: git reset --merge ORIG_HEAD // ORIG_HEAD指代了合并前的提交节点
            ```
        2. 在指定节点建立一个新的分支： git checkout -b <branchname> <commitID>
        3. 注意所有悬空的提交节点即：没有子节点指向它，且没有分支标签等指示的提交节点会被隐藏，但仍可通过reflog找回
    6. 在执行merge操作时如遇到冲突暂停，想撤销merge操作时
        1. git reset --merge HEAD  //该命令会回退到执行merge操作前的状态，并且能够保留原工作目录的状态。
    
    
5. git标签
    1. git标签分为轻量标签和附注标签，附注标签指添加了附注信息的标签
        ```
        git tag <tagname> [某个提交节点,默认为当前提交]
        git tag -a <tagname> [某个提交节点,默认为当前提交] -m 'message'   //-a 选项即指定为附注标签
        ```
    2. 运行push命令时标签并不会自动推送到远端仓库，需要手动指定
        ```
        git push origin [tagname]   //推送指定标签到远端仓库
        git push origin --tags      //推送所有标签
        ```
    3. 利用标签返回特定版本
        ```
        git branch -b <branchname> <tagname>  //通过新建一个分支来到达特定版本
        ```

6. git分支操作
    1. 分支的基本操作：
        - 查看分支： git branch -v
        - 新建分支： git branch <branchname> <commitid> 
        - 切换到某一分支：git checkout <branchname> <commitid>  //-b 选项可以执行创建分支并切换过去的操作
        - 删除分支： git branch -d <branchname>
        - 合并分支： git merge <branchname> //将指定的分支并入当前所在分支，若有冲突需要手动处理
    2. 合并冲突的处理：
        1. 若要合并的东西有冲突，git merge操作会提示需要手动处理，建议使用vscode来处理
        2. 冲突处理就是选择到底要保留哪些修改，处理完后进行git add 及 git commit 操作。
    3. 变基操作：
        1. 变基操作用于将分叉的提交历史合并，最终效果是使主分支能够直接快速合并新分支。
        2. 变基命令： git rebase <basebranchname>   //将当前所在分支变基到目标分支
            ```
            git rebase <basebranchname> [topbranchname默认指当前分支]
            ```
        3. 后续可以直接在目标分支快速合并至该分支。但对于原本有合并冲突的两个文件，采用上述变基操作后所有冲突的地方均采用了执行变基操作的分支。
        4. 对于合并操作推荐使用merge命令，只有在不会有合并冲突且需要修改提交历史时才采用变基操作。

## git 进阶命令
1. git reset
    1. git reset [tree-ish default:HEAD] <filepath>  // 将文件从暂存区撤销但仍保留在工作目录
    2. git reset [mode] [commitID]    //将当前分支恢复到指定节点，同时根据指定的模式可能会修改工作目录状态
        ```
           working index HEAD target         working index HEAD
           ----------------------------------------------------
            A       B     C    C     --soft   A       B     C
                                     --mixed  A       C     C
                                     --hard   C       C     C
                                     --merge (disallowed)
                                     --keep   A       C     C

           working index HEAD target         working index HEAD
           ----------------------------------------------------
            B       B     C    D     --soft   B       B     D
                                     --mixed  B       D     D
                                     --hard   D       D     D
                                     --merge  D       D     D
                                     --keep  (disallowed)

           working index HEAD target         working index HEAD
           ----------------------------------------------------
            B       B     C    C     --soft   B       B     C
                                     --mixed  B       C     C
                                     --hard   C       C     C
                                     --merge  C       C     C
                                     --keep   B       C     C

           working index HEAD target         working index HEAD
           ----------------------------------------------------
            B       C     C    D     --soft   B       C     D
                                     --mixed  B       D     D
                                     --hard   D       D     D
                                     --merge (disallowed)
                                     --keep  (disallowed)

           working index HEAD target         working index HEAD
           ----------------------------------------------------
            B       C     C    C     --soft   B       C     C
                                     --mixed  B       C     C
                                     --hard   C       C     C
                                     --merge  B       C     C
                                     --keep   B       C     C

        ```
2. commitID快速定位
    - HEAD：当前所在的分支
    - HEAD^ 或 HEAD~1 : HEAD前一个提交节点
    - HEAD~2 : HEAD前两个提交节点
    - ORiG_HEAD : 用于指代执行 git reset 后的原节点，同时也是在进行了pull，merge操作后原节点的位置。

3. git提交历史合并
    1. 如果需要修改提交历史使提交更具可读性可以进行如下步骤：
        ```
        git reset --soft <commitID>  //回退到项目的开始节点,所有修改回保留到暂存区，同时以前的提交历史将被隐藏
        git reset HEAD <file>        //将文件移出暂存区，以对暂存区内的文件进行阶段性的重现
        git reset HEAD               //移出所有文件，但仍保留在工作目录
        git add <file>               
        git commit                   //重复以上步骤，创建阶段性的提交历史
        ……
        ```

## git 内部原理
1. git内部实际存储的对象：数据对象(blob),树对象(tree),提交对象(commit)
    - blob对象对应单个文件
    - tree对象对应一个文件夹
    - commit对象对应一个项目最顶层的树对象(文件夹)和关于提交的信息(提交人，时间，说明等)

2. git引用。git内部利用SHA-1值来记录文件状态，为便于描述便产生了分支名，标签，其实质均只是一个位于.git/下的存储了SHA-1值的文件。
    - 所有用到分支名的地方都会自动解析成完整的：refs/heads/BRANCHNAME 的类似路径
        ```
        .git/refs/
        ├── heads   //该文件夹下存放本地仓库分支名文件
        │   ├── master
        │   └── rewrite
        ├── remotes  //该文件夹下存放远端仓库分支名文件
        │   └── origin
        │       └── HEAD
        └── tags     //该文件夹下存放标签名文件
        ```
    - .git/HEAD 文件则是一个符号引用指向了目前所在分支的名称
    - .git/config 文件可配置默认的git fetch,push 所要执行的分支名。
        ```
        [remote	"origin"]  //执行fetch操作时自动获取master和experiment分支。
            url	=	https://github.com/schacon/simplegit-progit
            fetch	=	+refs/heads/master:refs/remotes/origin/master
            fetch	=	+refs/heads/experiment:refs/remotes/origin/experiment
        ``` 
        ```
        [remote	"origin"]  //执行push时自动将本地的master分支推送至远端的master分支
            url	=	https://github.com/schacon/simplegit-progit
            fetch	=	+refs/heads/*:refs/remotes/origin/*
            push	=	refs/heads/master:refs/heads/qa/master
        ```
3. git commit 操作会产生并存入一个提交对象，利用这个提交对象可以进行完整的复原
    - 只需要知道提交对象的SHA-1值便可以通过 git reset --hard <SHA-1> 回退到该节点
    - 或者使用 git branch <BRANCHNAME> <SHA-1> 在指定节点设立一个新的分支
    - 至于如何查找SHA-1值，可以用git reflog，git log 等命令获取

4. git 提交历史里出现过的文件会一直保留在仓库中，如果要想彻底删除需要修改提交历史。
