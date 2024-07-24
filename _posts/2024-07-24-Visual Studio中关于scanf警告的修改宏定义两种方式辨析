---
layout:     post
title:      scanf警告的修改宏定义行为
subtitle:   在Visual Studio中的两种方式辨析
date:       2024-07-24
author:     ZT
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Blog
---

 

1.问题引入
------

        在下载VS后，我们不可避免的需要对其进行兼容性配置。其中最重要的一条就是避免[scanf函数](https://so.csdn.net/so/search?q=scanf%E5%87%BD%E6%95%B0&spm=1001.2101.3001.7020)出现如下所示的警告信息：

![](https://img-blog.csdnimg.cn/direct/d230684eac1f48fc885dfe89f0ade281.png)        

        这通常是由于Visual Studio基于[安全性](https://so.csdn.net/so/search?q=%E5%AE%89%E5%85%A8%E6%80%A7&spm=1001.2101.3001.7020)考虑，对ANSI的库函数进行了限制，强制使用其自带的函数，而这种做法通常情况下并不值得肯定，不仅会影响代码的兼容性，也极易恐吓到刚入门的新手们。   

        具体到本问题则是标准函数scanf()在对字符数组以%s格式输入时并不检查边界，从而带来了越界溢出的风险，因此Microsoft强制要求使用自带的scanf_s()函数来进行替换，该函数要求输入时有一个第三参数size来确保输入的字符串长度不超过size。

2.解决问题
------

        当我发现警告时，我在老师的教案和网络的解答中得到了两种一劳永逸的修改方法（在不改变项目的前提下），二者仅有细节的不同。都是从宏定义的修改方面入手，具体步骤参见[http://t.csdnimg.cn/JjeM3](http://t.csdnimg.cn/JjeM3 "http://t.csdnimg.cn/JjeM3")中的第三、四点方法。

![](https://img-blog.csdnimg.cn/direct/74357908db7c432c9770336b8ffb2b27.png)​        

        今天我要讨论的是\_CRT\_SECURE\_NO\_WARNINGS和\_CRT\_SECURE\_NO\_DEPRECATE有什么区别。

3.区别辨析
------

_       " \_CRT\_SECURE\_NO\_WARNINGS" 和" \_CRT\_SECURE\_NO\_DEPRECATE"是在C/C++编程中与微软的C运行时库（CRT）相关的预处理器定义。它们用于控制在编译程序时是否生成关于不安全或过时函数的警告。_

###   
3.1  \_CRT\_SECURE\_NO\_WARNINGS

        这个宏用于关闭所有由CRT库生成的关于不安全函数的警告。  
        当使用一些被认为不安全的函数（如\`strcpy\`、\`sprintf\`等，它们容易导致缓冲区溢出）时，编译器会发出警告。定义这个宏后，这些警告将被抑制。  
        使用这个宏意味着开发者接受使用这些不安全函数的风险，并选择不处理相关的警告。

###   
3.2  \_CRT\_SECURE\_NO\_DEPRECATE

        这个宏用于关闭所有由CRT库生成的关于已弃用函数的警告。  
        当使用一些已经被标记为弃用的函数时，编译器会发出警告。定义这个宏后，这些警告将被抑制。

        弃用的函数可能是因为有更安全或更有效的替代品，或者因为它们可能在未来的库版本中被移除。

4.总结
----

        总的来说，`\_CRT\_SECURE\_NO\_WARNINGS` 主要用于关闭与安全相关的警告，`\_CRT\_SECURE\_NO\_DEPRECATE` 用于关闭与函数弃用相关的警告。使用这些宏可以帮助开发者管理他们的代码警告，但同时也意味着可能忽视了潜在的安全或维护问题。因此，在决定使用这些宏之前，应该仔细评估代码的安全性和长期维护需求。

        个人认为以第二种描述为宜，相对来说错误可能更少。当然也可以直接采用修改C++模版文件的方式来解决。
