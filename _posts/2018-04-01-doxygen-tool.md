---
layout: post
title:  "按照Doxygen工具规范给程序添加注释"
date:   2018-04-01 16:14:54
categories: Tools
tags: Tools Doxygen 
---

* content
{:toc}

Doxygen工具用于生成软件文档是十分方便的。




# Doxygen工具介绍
先引用帮助文档中的一段话：Doxygen is the de facto standard tool for generating documentation from annotated C++ sources, but it also supports other popular programming languages such as C, Objective-C, C#, PHP, Java, Python, IDL (Corba, Microsoft, and UNO/OpenOffice flavors), Fortran, VHDL, Tcl, and to some extent D.
对于英文不太好的同学，做以下解释：Doxygen是一个可以从带注释的C++（C、Python、Java等语言）源文件产生标准文档的工具。
# 为什么要用这个工具
那先从拿自己开刀吧，对于自己刚刚接触编程的时候，当初并没有太重视对注释的编写（可以是因为当时别人也不会看我的程序，只要自己明白就OK了）。随着自己编写的程序越来越多以及工作后需要共享你写的代码给其他同事使用得时候，问题就逐渐的暴露出来了。啊，自己也会对自己写的代码变得陌生！！！还有就是共享代码问题，别人拿到你的代码基本上都要去问你一次代码应该如何应用的他自己的工程中，对于两个问题主要的原因就是自己写的程序没有注释或者注释不够明了。后来我就去寻找一些相关书籍去看，包括程序的变量名如何命名，注释如何规范等等相关书籍。从此以后我开始注重自己编写程序的规范化。再一次偶然的机会中看到了Doxygen工具，原来它可以将你编写的程序直接生成文档，以后你再给其他人共享程序的时候，别人再也不用逐行看你的代码了，直接看此文档就可以了，也免去了解释，节省了大家的时间，何乐而不为呢？
还有另外一个重要的原因可以在一定程度上提升你的工资水平，这个可是实实在在的物质奖励。
从另外一个角度来看，能够把注释写好的程序员，其写的程序也不会差！！！
闲话少说直接上干货
# Doxygen注释规范
如果想使用此工具必须按照它的规范来编写注释，这就是所谓的入乡随俗吧，哈哈。

 1. 常用标记
    @author         作者 
    @brief             简要
    @version         版本号
    @date             日期
    @file                文件名，可以默认为空，DoxyGen会自己加
    @param           函数参数
    @return           函数返回值描述
    @exception      函数抛异常描述
    @warning         函数使用中需要注意的地方
    @remarks        备注 
    @see               参考字段
    @since             从哪个版本后开始有这个函数的
    @todo             被标记的代码会在ToDo列表中出现
 
 2. 使用例子

    a、文件注释例子
```
    /** @file file.h
     * @brief A brief file description.
     * A more elaborated file description.
     */
```
   b、变量的注释
   使用///< 表示需要注释的内容在注释前面，使用///表示需要注释的内容在注释后面。

```
   /// 这是一个枚举
   enum EnumType
    {
      int EVal1,     ///< enum value 1 
      int EVal2      ///< enum value 2
    };
```

```
/** 
  * @brief  GPIO Configuration Mode enumeration 
  */   
typedef enum
{ 
  GPIO_Mode_IN   = 0x00, ///< GPIO Input Mode */
  GPIO_Mode_OUT  = 0x01, ///< GPIO Output Mode */
  GPIO_Mode_AF   = 0x02, ///< GPIO Alternate function Mode */
  GPIO_Mode_AN   = 0x03  ///< GPIO Analog Mode */
}GPIOMode_TypeDef;
```

c、函数注释

```
/** @fn const char *Fn_Test::member(char c,int n) 
 *  @brief A member function.
 *  @param c a character.
 *  @param n an integer.
 *  @exception std::out_of_range parameter is out of range.
 *  @return a character pointer.
 */
 const char *Fn_Test::member(char c,int n) throw(std::out_of_range) {}
```

```
/**
  * @brief  Fills each GPIO_InitStruct member with its default value.
  * @param  GPIO_InitStruct : pointer to a GPIO_InitTypeDef structure which will be initialized.
  * @return None
  */
void GPIO_StructInit(GPIO_InitTypeDef* GPIO_InitStruct)
{
  /// Reset GPIO init structure parameters values
  GPIO_InitStruct->GPIO_Pin  = GPIO_Pin_All;
  GPIO_InitStruct->GPIO_Mode = GPIO_Mode_IN;
  GPIO_InitStruct->GPIO_Speed = GPIO_Speed_2MHz;
  GPIO_InitStruct->GPIO_OType = GPIO_OType_PP;
  GPIO_InitStruct->GPIO_PuPd = GPIO_PuPd_NOPULL;
}
```
以上注释只是说明了几种比较常用的注释例子，关于如何书写格式更丰富的内容请参考官方文档。大家看了此类注释是不是比较舒服，那就简单学习一下doxygen的注释规范吧！规范也支持应用广泛的Markdown格式。

以后有时间的话，我再更新一篇如何使用doxygen生成程序标准文档的博客。使用其生成的文档形式还是比较丰富的，甚至还有函数调用关系图。此博客只是抛砖引玉，Doxygen的功能远远大于文中提到功能。