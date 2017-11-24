# python 基础知识
>[python官网](https://docs.python.org/3/tutorial/index.html)

## 1. Input&Output
1. str()和repr()的区别：
str()转化成人可读的，repr()只是硬性转化成字符
    
        >>> # The repr() of a string adds string quotes and backslashes:
        ... hello = 'hello, world\n'
        >>> hellos = repr(hello)
        >>> print(hellos)
        'hello, world\n'    //用str()则可以将\n转化成换行
