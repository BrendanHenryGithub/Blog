# markdown 语法简介

## markdown 主要元素

### 列表
1. 有序表 
2. 无序表
    - 列表可嵌套
    - ……

### 表格
|序号|内容|
|-------|--|
|1.     |……|
|2.     |……|
|3.     |……|
|4.     |……|

### 图片
![Alt text](/path/to/img.jpg)

### 链接
[Link to baidu.com](http://www.baidu.com)

### 文本修饰
1. **粗体**
2. *斜体*
3. ~~删除~~

### 代码片段
```javascript
function fancyAlert(arg){
    if(arg){
        $.facebox({div:'#foo'})
    }
}
```

    def foo():
        if not bar:
            return True

### 引用
> 引用的参考资料

### github markdown扩展功能
1. 选项列表
    - [ ] This is a incomplete item
    - [x] This is a complete item
2. emoji 小图标
    - :sparkles: :camel: :boom:
3. @链接
    - @用户名

### markdown额外的可扩展功能
1. markdown可解析所有html标签
2. markdown可以利用扩展插件支持LaTex语法(如：显示数学公式)


