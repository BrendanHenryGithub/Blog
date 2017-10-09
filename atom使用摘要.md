# atom使用总结
>本总结使用Markdown语法

## 快捷键
### atom快捷键
- 新建文档 : ctrl+N
- 保存文档 : ctrl+S
- 调出设置界面 : ctrl+,
- 显示Markdown预览 : ctrl+shift+M
- 显示文件树 : ctrl+\
- 聚焦文件数 : alt+\
- 添加文件树目录 : ctrl+alt+O
- 开启快捷键检测 : ctrl+.
- 命令查询 : ctrl+shift+P
- 文件跳转面板 : ctrl+T
- HTML预览 : ctrl+shift+H
- 分屏 : ctrl+w ctrl+v (向右分屏)
- 分屏 : ctrl+w ctrl+s (向下分屏)
- 切换分屏: ctrl+w w(下一个分屏)  
- 打开前一个关闭的页面 : ctrl+shift+T
- 代码块折叠 : ctrl+alt+[
- 代码块展开 : ctrl+alt+]
- 分屏 : ctrl+k 方向键
- 注释代码：Ctrl+/

### vim快捷键
- 粘贴 : P(行前) p(行后)
- 拷贝当前行 : yy
- 到行头 : 0
- 到行尾 : $
- 到行头第一个非空格元素 : ^
- 到行尾第一个非空格元素 : g_
- 重复上次命令 : .
- 跳到第一行 : gg
- 跳到最后一行 : G
- 到下一个单词的词头 : w  W(以空格为界限)
- 到下一个单词的词尾 : e  E(以空格为界限)
- 匹配符号移动 : % (要先移动到相应符号处({[))
- 匹配当前光标所在单词 : \*(到下一个) #(到上一个)
- 到本行的,前一个字符 : t,
- 到本行的a的前一个字符 : fa
- 删除所有的内容直到遇到双引号 : dt"
- 代码块折叠：zc
- 代码块展开：zo
- 合并下一行：shift+j

### terimal快捷键
- 光标跳至行首：ctrl+a
- 光标跳至行尾：ctrl+e
- 剪贴行首内容至光标：Ctrl+u
- 剪贴行尾内容至光标：Ctrl+k
- 粘贴剪贴内容：Ctrl+y
- 显示上一条（下一条）历史命令：Ctrl+p（n）
- 光标前移（后移）：Ctrl+b（f）
- 清屏：ctrl+l
- 新建选项卡：Ctrl+shift+t
- 关闭选项卡：Ctrl+shift+w
- 打开atom中terimal：alt+shift+T
- 关闭atom中terimal: alt+shift+x

## atom扩展
### 通用插件
- vim-mode-plus(比vim-mode支持更多命令)
- minimap : 代码小地图
- git-plus : git扩展
- blacket-close-jump: （快捷键tab）跳出括号
- Atom beautify: 代码美化(html默认支持，c++需手动配置)快捷键：ctrl+alt+j
- file-icons : 文件图标插件
- platform-ide-terminal : atom终端插件
- indent-guide-improved : 缩进指引显示
- linter : 代码检查插件（需配合具体语言插件使用）
### 前端插件
- emmet : html编辑扩展
- color-picker : 颜色选择插件
- javascript-snippets : javascript代码片段
### Python插件
- linter-flake8 : python代码检查插件
- autocomplete-python : python代码自动补全
- python-tool : python代码辅助工具(alt+j:跳转至相应函数的定义处)

### 文本编辑类插件
- markdown-preview-plus : markdown扩展
### c/c++ 插件
- clang fromat : 格式化排版代码
- linter系 : 代码检查和错误提示(如c++语言还需安装配套的语法文件linter-gcc,其他还需ui插件)
- autocomplete-clang:借助clang编译器的c++自动补全插件
- dbg系：利用gdb调试c++代码
- gpp-compiler: 编译执行

## atom快速更新与安装
- sudo add-apt-repository ppa:webupd8team/atom
- sudo apt-get update
- sudo apt-get install atom  (注意安装完后需要修改成普通用户权限即/home/john/.atom/compile-cache/less/df1b7fbc57dbeed23a8f1f8de95b4dfebcc06066/imports.json下的imports.json的权限！并且在sudo下运行会出现输入法错误问题！！)

## Snippets-扩展代码块
>可参考[Snippets](http://zkread.com/article/653578.html)
