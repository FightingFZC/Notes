---
title: NO.5 数组Array
updated: 2021-05-02T12:37:18.0000000+08:00
created: 2021-01-29T18:05:59.0000000+08:00
---

数组Array
# Java中的数组
1.  Java语言中的数组是一种引用数据类型。不属于基本数据类型。数组的父类是Object
2.  数组实际上是一个容器，可以同时容纳多个元素。（是一个数据的集合）
3.  数组当中可以存储基本数据类型的数据，也可以储存引用数据类型的数据。
4.  数组因为是引用类型，所以**数组对象是堆内存当中**

# Java中数组的声明
1.  声明/定义一个一维数组
数据类型\[\] 数组名;

如：int\[\] array1;

double\[\] array2;
2.  初始化一个一维数组：
    1.  静态初始化：int\[\] array = {100, 2100, 300, 55};//也可以想C语言那样定义：int array\[\]
    2.  动态初始化：int\[\] array = new int\[5\];//int array\[\] = new int\[5\]也行//二位数组：new int\[5\]\[7\]
PS:**初始化后会赋上默认值。**

越界后会出现ArrayIndexOutOfBoundsException数组下标越界异常

二维数组就多一个\[\]，且二维数组名.length为其一维数组的个数
3.  一旦创建，长度不可变，不过可以用System.arraycopy(源数组名，起始位置，目标数组名，目标数组的起始位置，拷贝长度)扩容需要创建一个大数组，然后一个个拷贝进去（是钱拷贝）。
4.  和C一样，一般只有一维数组和二维数组，**下标从0开始**
5.  所有的数组都有length属性，表示数组的长度。
6.  数组中元素的地址是连续的，引用储存的地址是首地址
**优点**
1.  查询效率最高！
2.  有首地址，内存类型，有下标，查询非常方便。
**缺点**
1.  由于为了保证数组连续，随机删减的时候效率低，因为需要把前后所有元素向前移或者向后移
2.  很难在内存空间找到一块特别大的连续的空间去储存一个大数据量
# Java中数组的使用
1.  在调用一个方法写实参时可以是：数组名，new int\[5\] ，int\[\]{1,2,3}
2.  main方法中的String\[\] args，在IDEA中的Run-\>Edit Configuration中的Program arguments里可以设置，DOS运行就是java 类名 xxx xxx xxx xxx用空格分开传进去，所以String\[\] args是动态的，输入几个，长度就是多少（可以当用户名和密码（手动滑稽））
