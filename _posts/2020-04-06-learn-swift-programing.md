---
layout: post
title:  "30分钟入门Swift语言简明教程"
description: X分钟学习swift简要语言教程
date:   2020-04-06 10:40:00 +0800
category: tools
tags: [swift, 简要教程]
---

作为一个有多年编程经验的熟练工程师，学习一门新语言的成本应该是非常低的。下面我将学习swift语言的过程记录下来，及帮助自己做个笔记，也帮助swift新手们尝鲜。


## 学以致用

首先要时刻铭记，学习的目的就是为了在实践中应用，要带着问题和目的去学习，而不是为了学习而学习。

根据我的经验，最好的学习路径应该是：
**学习 -> 实践 -> 遇到问题 -> 学习 -> 实践 ...**



## 准备内容

一台安装了Xcode的Mac电脑。



## 开始学习

### 1- Hello World

老规矩，先从hellow world程序开始。

```
var myString = "Hello, World!"
 
print(myString)
```

看起来，语言还是比较简洁讨人喜欢的。参数使用的var，和JS一样。而打印方法和python 3是一样的。

重点的是我们了解到，**swift语言是不强制使用分号结尾的**。

### 2- 基础语法

**定义变量**

直接关键字 var，无需关注数据类型可以直接赋值，和js看起来是一样的。

```
        var msg = "\n hello world \n"
        var num = 1984  // 数字
        var float_num = 1999.0 // 浮点数字
        var flag = true // 布尔类型
        // 可变类型，重复赋值
        num = 1997
        float_num = 2012.01
```

使用关键字 let 来定义常量，效果通Java中的 final。

值得注意的是，虽然swift看起来像解释性语言一样方便，但是实际上他还是强类型的语言。可以强制定义其数据的类型。
```
        var msg:String = "\n hello world \n"
        var num:Int = 1984  // 数字
        var float_num:Float = 1999.0 // 浮点数字
        var flag:Bool = true // 布尔类型
```

**数组**

创建数组方式一，以下实例创建了一个类型为 Int ，数量为 3，初始值为 0 的空数组：

```
var someInts = [Int](repeating: 0, count: 3)

```

创建数组方式二：

```

var someInts:[Int] = [10, 20, 30]
```

可以直接使用下标访问数组，下标从0开始。新增元素可以用使用append方法或者直接 +=

```
        var someInts = [Int]()
        someInts.append(20) // 添加 20
        someInts.append(30)	// 添加 30
        someInts += [40]	// 添加 40
```

> 数组的长度使用 count 属性; isEmpty来判断是否为空数组。


**字符串**

掌握字符串的处理是入门一个开发语言的基本操作，因此要重点学习下字符串处理相关的方法。


```
var greeting = "Hi"
var name = "jack"

var msg = greeting + " " + name
print(msg) // Hi jack
var msg2 = "\(greeting) \(name)"
print(msg2) // Hi jack

print(msg == msg2) // true

```

格式化字符串和数字时候直接使用 "\(parm)"来替代既可以，非常方便。

> 属性count和isEmpty在字符串处理同样适用。


**关于nil**

代表空的指针，和java中的null、python中的None相同。


**运算符**

包含多种运算符，例如：算术运算符、关系运算符、逻辑运算符、位运算符、赋值运算符及其他运算符。基本与其它高级语言无区别，再此不做多余记录。


> 注意：swift3 中已经取消了++、--。


**注释**

```
//这是一行注释
/* 这也是一条注释，
但跨越多行 */
```

### 程序结构

程序的3中结构：顺序、选择和循环。下面看一下如果来处理选择和循环。

**选择**

不需要括号包含布尔表达式, 其它与Java相同。

```
if boolean_expression {
   /* 如果布尔表达式为真将执行的语句 */
}

var a = 1 

// && = 与 ， || = 或
if a  < 10 {
	print("a 小于 10")
}

```

**循环**

循环数组

```
var someStrs = [String]()

someStrs.append("Apple")
someStrs.append("Amazon")
someStrs.append("Runoob")
someStrs += ["Google"]

// 仅元素
for item in someStrs {
   print(item)
}

// 元素与下标
for (index, item) in someStrs.enumerated() {
    print("在 index = \(index) 位置上的值为 \(item)")
}
```

循环字符串

```
for ch in "Runoob" {
    print(ch)
}
```

其余与其它语言无异同。


### 数据结构

数组刚才已经提到了，下面讲解下字典（对应Java里的Hash table)

```
    	var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
        var someVar = someDict[1]  // 访问字典元素

        someDict.updateValue("One 新的值", forKey: 1) // 修改字典元素

        var removedValue = someDict.removeValue(forKey: 2) // 删除字典元素
        
        // 遍历字典
        for (key, value) in someDict {
           print("字典 key \(key) -  字典 value \(value)")
        }
        
        let dictKeys = [Int](someDict.keys) // 所有的key
        let dictValues = [String](someDict.values) // 所有的value

        print("输出字典的键(key)")
        print("输出字典的值(value)")
```


### 内置库

排序
字符串

```
import Cocoa

var name = "菜鸟教程"
var site = "http://www.runoob.com"

print("\(name)的官网地址为：\(site)")
```


### 面向对象(或函数式编程)


### 高级特性
TBD

## 总结












