Tags：ES6学习总结

## Learning Summary In ES6

 - [(一) 变量与字符串](#一-变量与字符串)

### (一) 变量与字符串

 1. let 变量

    - let 的作用类似于 var , 用来声明变量, 但是所声明的变量, 只在 let 命令所在的代码块内有效, 例如: 
    
       ```javascript
        if(true){
            var a = 1;
            let b = 2;
        }
        console.log(a);                 //输出为1
        console.log(b);                 //报错: ReferenceError: b is not defined
       ```
       
    - let 声明的变量会有声明提升, 例如: 
    
      ```javascript
        console.log(a);                 //undefined
        console.log(b);                 //undefined
        var a = 10;
        let b = 10;
      ```
      
    - 在for循环的计数器中, 很适合使用 let 命令声明的变量, 例如:
    
      ```javascript
        var a = []; 
        for(let i = 0; i<10;i++){
            a[i] = function(){
                console.log(i);
            }
        }
        a[3]();                             //输出的为: 3 
      ```
 
 2. const 常量
 
    - const 声明的是常量, 一旦声明, 值将是不可变的, 例如: 
    
      ```javascript
        const i = 10;
        i = 1;                      //报错
        const i = 5;                //报错
      ```
      
    - const 也是具有块级作用域
    
      ```javascript
        if(1){
            const i = 10;
        }
        console.log(i);             //报错: ReferenceError
      ```
      
    - const 声明的常量能变量提升 ( 必须先声明后使用 ) , 例如:
    
      ```javascript
        if(1){
            console.log(a);         //输出为 undefined
            const a = 10;
        }
      ```
      
    - const 不可重复声明, 例如:
    
      ```javascript
        var message = "Hello!";
        let age = 25;
 
        // 以下两行都会报错
        const message = "Goodbye!";
        const age = 30;
      ```
     
    - const 指令指向变量所在的地址，所以对该变量进行属性设置是可行的（未改变变量地址），如果想完全不可变化（包括属性），那么可以使用冻结, 例如: 
    
      ```javascript
        const C1 = {};
        C1.a = 1;
        document.write(C1.a);       // 1 
        C1 = {};                    // 报错  重新赋值，地址改变
         
        //冻结对象，此时前面用不用const都是一个效果
        const C2 = Object.freeze({}); 
        C2.a = 1;                   //Error,对象不可扩展
        document.write(C2.a);
      ```

 3. 是否包含字符串的三种新方法
 
    传统上, javascript 只有 indexOf() 方法, 可以用来确定一个字符串是否包含在另一个字符串中, 在ES6中又提供了三种新方法: 

    - includes() : 
    
      返回布尔值, 表示是否找到了参数字符串, 例如: 
      
      ```javascript
        var str = "Hello World";
        str.includes("o");                      // 返回true
      ```
      
    - startsWith() : 
    
      返回布尔值, 表示参数字符串是否在源字符串的头部, 例如: 
      
      ```javascript
        var str = "Hello World";
        str.startsWith("o");                    // 返回false
      ```
      
    - endsWith() : 
    
      返回布尔值, 表示参数字符串是否在源字符串的尾部, 例如: 
      
      ```javascript
        var str = "Hello World";
        str.endsWith("ld");                     // 返回true
      ```
      
    - 另外, 这三个方法都支持第二个参数, 表示开始搜索的位置, 例如: 
    
      ```javascript
        var str = "Hello World";
        str.includes("o", 6);                   // 返回true
        str.startsWith("or", 6);                // 返回false
        str.endsWith("ld", 6);                  // 返回true
      ```
      在上面的代码里面, 可以看出, 对于第二个参数, endsWith() 方法与其他两个方法有所不同, 它针对的是前 n 个字符, 而其他两个方法针对的是从第 n 个位置直到字符串结束;