---
layout: post
title:  "QT实现对指定文件夹内文件类型过滤功能"
date:   2018-05-04 16:14:54
categories: QT
tags: QT  QFileSystemModel
---

介绍使用QFileSystemModel类实现文件过滤功能

1、代码如下
``` 
    dirmodel=new QFileSystemModel();  
    dirmodel->setRootPath(QDir::currentPath());//设置根目录  
    
    QStringList strlist;  
    strlist<<QString("*.jpg");  
    dirmodel->setNameFilters(strlist);  
    dirmodel->setNameFilterDisables(false);//true表示不符过滤器要求的项目变灰，不能选中，false表示不符合要求的直接不显示  
    
    ui->listView->setModel(dirmodel);  
    ui->listView->setRootIndex(dirmodel->index(QDir::currentPath()));//设置显示目录
```
dirmodel 是QFileSystemModel的一个实例，如果过滤选项发生变更，只需要重新对dirmodel设置过滤器即可。

2、提取文件名
```
qDebug()<<dirmodel->fileName(index); 
```
