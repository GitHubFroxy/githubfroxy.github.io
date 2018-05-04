---
layout: post
title:  "QByteArray用法小总结"
date:   2018-05-04 16:14:54
categories: QT
tags: QT  QByteArray
---

QByteArray用法小总结


1、代码如下
``` 
     QByteArray array;  
    array.resize(3);  
      
    array[1]=0x7f;  
    qDebug("I array[1]=0x7f;array 1 is %d,%x",QVariant(array[1]).toInt(),QVariant(array[1]).toInt());  
    qDebug("I array[1]=0x7f;__array 1 is %d,%x",array.at(1),array.at(1));  
    qDebug("I array[1]=0x7f;___array 1 is %d,%x",QVariant((unsigned char)array[1]).toInt(),QVariant((unsigned char)array[1]).toInt());  
      
    array[1]=0xff;  
    qDebug("II array[1]=0xff;array 1 is %d,%x",QVariant(array[1]).toInt(),QVariant(array[1]).toInt());  
    qDebug("II array[1]=0xff;__array 1 is %d,%x",array.at(1),array.at(1));  
    qDebug("II array[1]=0xff;___array 1 is %d,%x",QVariant((unsigned char)array[1]).toInt(),QVariant((unsigned char)array[1]).toInt());  
      
    array[1]=0x000000ff;  
    qDebug("III array[1]=0x000000ff;array 1 is %d,%x",QVariant(array[1]).toInt(),QVariant(array[1]).toInt());  
    qDebug("III array[1]=0x000000ff;__array 1 is %d,%x",array.at(1),array.at(1));  
    qDebug("III array[1]=0x000000ff;___array 1 is %d,%x",QVariant((unsigned char)array[1]).toInt(),QVariant((unsigned char)array[1]).toInt());  
      
    array[1]=-127;  
    qDebug("IV array[1]=-127;array 1 is %d,%x",QVariant(array[1]).toInt(),QVariant(array[1]).toInt());  
    qDebug("IV array[1]=-127;__array 1 is %d,%x",array.at(1),array.at(1));  
    qDebug("IV array[1]=-127;___array 1 is %d,%x",QVariant((unsigned char)array[1]).toInt(),QVariant((unsigned char)array[1]).toInt());  
      
    array[1]=0x7f01;  
    qDebug("V array[1]=0x7f01;array 1 is %d,%x",QVariant(array[1]).toInt(),QVariant(array[1]).toInt());  
    qDebug("V array[1]=0x7f01;__array 1 is %d,%x",array.at(1),array.at(1));  
    qDebug("V array[1]=0x7f01;___array 1 is %d,%x",QVariant((unsigned char)array[1]).toInt(),QVariant((unsigned char)array[1]).toInt());  
```
输出结果是：
```
I array[1]=0x7f;array 1 is 127,7f
I array[1]=0x7f;__array 1 is 127,7f
I array[1]=0x7f;___array 1 is 127,7f

II array[1]=0xff;array 1 is -1,ffffffff
II array[1]=0xff;__array 1 is -1,ffffffff
II array[1]=0xff;___array 1 is 255,ff

III array[1]=0x000000ff;array 1 is -1,ffffffff
III array[1]=0x000000ff;__array 1 is -1,ffffffff
III array[1]=0x000000ff;___array 1 is 255,ff

IV array[1]=-127;array 1 is -127,ffffff81
IV array[1]=-127;__array 1 is -127,ffffff81
IV array[1]=-127;___array 1 is 129,81

V array[1]=0x7f01;array 1 is 1,1
V array[1]=0x7f01;__array 1 is 1,1
V array[1]=0x7f01;___array 1 is 1,1
```
由代码及结果看出，

1.QByteArray 中的元素有32位，但在赋值时`array[]`仅仅只存储被赋的值的低8位，`array[]`中剩下的高位24位则按照低八位的最高位统一补0或者1

2.QByteArray 中的元素有符号

3.QByteArray赋值时仅仅能使用`array[i]=value`;这种形式，`array.at(i)`是只读的，并且强制类型转换对array.at(i)不起作用。

4.若要读取使用其元素值，如果要获取有符号数形式，`QVariant(array[i]).toInt()`与`array.at(i)`等价。如果获取其元素值的无符号数形式，需要`QVariant((unsigned char)array[i]).toInt()`。

5.`array.data()`指向其存储的char*