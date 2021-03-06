---
layout: post
category: Andraw-lin
title: About Others
summary: About Others
---

## **其他类型整体总结**

 - [(一) 栈(stack)和队列(queue)区别](#一-栈stack和队列queue区别)
 - [(二) 栈(stack)和堆(heap)的区别](#二-栈stack和堆heap区别)
 - [(三) 快排实现](#三-快排实现)
 - [(四) Jquery源码简单分析](#四-jquery源码简单分析)
 - [(五) ES6简单了解](#五-es6简单了解)

### (一) 栈(stack)和队列(queue)区别

 1. 栈的插入和删除操作都是在一端进行的，而队列的操作却是在两端进行的;
 2. 栈先进后出, 队列先进先出;
 3. 栈只允许在栈顶一端进行插入和删除，而队列只允许在表尾一端进行插入，在表头一端进行删除
 

### (二) 栈(stack)和堆(heap)区别

 1. 栈区: 由编译器分配释放, 存放函数的参数值, 局部变量的值等;
 2. 堆区: 一般由程序员分配释放, 若程序员不释放, 程序结束时可能由OS回收;
 

### (三) 快排实现

"快速排序"的思想:

 1. 在数据集之中, 找一个基准点(一般是第一个元素或者最后一个元素);
 2. 建立两个数组, 然后右指针找比基准数小的，左指针找比基准数大的, 通过几次比较交换后, 两个指针会相遇在一个数上, 然后与基准数交换;
 

### (四) Jquery源码简单分析

 1. 源码都封装在IIFE(自执行函数)里面;
 2. 原型属性和方法封装到了jquery.prototype里面;
 3. 将全局window对象作为参数传入(当jquery中访问window对象的时候，就不用将作用域链退回到顶层作用域了，从而可以更快的访问window对象);
 

### (五) ES6简单了解

 1. ####let 和 const 变量声明: 
    有效地解决了原来 var 的缺陷以及一些问题, 包括: 
    - 块级作用域 ;
    - 变量提升 ;
    - 定义常量问题 ;

 2. ####变量的解构赋值: 
    - 方便交换两个变量的值 ;
    - 解决了函数返回多个值 ;
    - 方便提取JSON数据等 ;
 
 3. ####字符串的扩展: 
    - 新增各种处理字符串的方法: 
      有效解决了 ES5 中对字符串处理的缺陷, 新增了多种处理方法, 例如, 在 ES5 中只能通过 indexOf ( ) 方法确定一个字符串是否包含在字符串, 但在 ES6 中则新增了 includes ( )(是否找到了参数字符串, 返回布尔值), startsWith ( )(参数字符串是否在源字符串的头部, 返回布尔值), endsWith ( ) ;

    - 补全字符串: 
      当然在 ES7 推出了字符串补全长度的功能, 即如果某个字符串不够指定长度, 会在头部或尾部补全, padStart 用于头部补全, padEnd 用于尾部补全 ;
    
    - 模板字符串: 
      另外在 ES6 中还推出了模板字符串, 有效地解决了在 ES5 中只能通过 + 号来拼接字符串 ;
    
 4. ####函数的扩展
    - 解决了 ES5 中在函数无法直接给参数设置默认值 ;
    - 添加了 rest 参数, 形式为" ...变量名 ", 用于获取函数的多余参数 ;
    - 扩展运算符 ( ... ), 好比如 rest 参数逆运算, 将一个数组转为用逗号隔开的参数序列 ;
    - ( 重点 ) 添加了箭头函数, 把回调函数 ( callback ) 表达得更加简洁, 另外箭头函数内不存在 this 对象 ( 不可以使用 new 命令, 不可以使用 arguments 对象, 不可以 yield 命令 ) ;

 5. ####Symbol类型
    用于定义一个独一无二的值, 可以保证不会与其他属性名产生冲突;

 6. ####Set和Map数据结构
    - set结构类似数组, 但成员的值都是唯一的, 没有重复值;
    - WeakSet 结构与Set类似, 不能出现重复的集合, 区别就是WeakSet中的对象之鞥是对象, 不能是其他类型的值;
    - Map结构解决了 ES5 中只能用字符串当作键的缺陷, 允许各种类型的值包括对象都能当作键;
    - WeakMap只接受对象作为键名 ( null除外 ) ;

 7. ####Generator函数

    - 从语法上, 可以理解Generator函数是一个状态机, 封装了多个内部状态 ; 
    - 执行Generator函数会返回一个遍历器对象, 因此Generator函数除了状态机, 还是一个遍历器对象生成器, 通过next()方法进行遍历 ;
    

 8. ####Promise对象
    有效地解决 Ajax 回调函数多层嵌套的问题, 通过 then 方法执行对应状态的回调函数, 每个 then 方法都会返回Promise对象, 采用链式的 then , 使得代码看起来是纵向发展的, 而不是像 Ajax 多层嵌套那样横向发展的 ;