Tags：ES6学习总结

## Learning Summary In ES6

 - [(一) 变量与字符串](#一-变量与字符串)
 - [(二) 数值](#二-数值)
 - [(三) 数组](#三-数组)

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

 4. repeat () 方法
 
    repeat () 返回一个新字符串, 表示将原字符串重复 n 次, 例如: 

    ```javascript
        var str = "Andraw-lin";
        console.log(str.repeat(2));     //输出: Andraw-linAndraw-lin    
    ```
    
 5. 模板字符串

    - 模板字符串中, 支持字符串的插值, 例如:
    
      ```javascript
        let name = "Andraw-lin";
        $("#test").append(`Hello ${name}`);     //输出: Hello Andraw-lin
      ```
      
    - 模板字符串还可以包含多行, 例如: 
    
      ```javascript
        let multiLine = `
            This is
            a string
            with multiple
            lines
            `;
        document.write(multiLine);  
      ```
 
 6. 标签模板
 
    先举个例子: 

    ```javascript
        var a = 5,
            b = 10;
        tag`Hello ${a+b} world ${a*b}`;     //注意, 前面的tag可以换成自定义名字
    ```
    
    由上面的代码可以看出, 模板字符串前面有一个标识名, 它是一个函数, 整个表达式的返回值, 就是tag函数处理模板字符串后的返回值, 这时候tag函数的所有参数的实际值如下: 
    
    - 第一个参数: ["Hello ", 'world '];
    - 第二个参数: 15 ( 即a+b的结果 );
    - 第三个参数: 50 ( 即a*b的结果 );
    
    下面是一个完整的例子程序: 
    
    ```javascript
        var a = 5,
            b = 10;
        function tag(s, v1, v2){
            document.write(s[0]);
            document.write(s[1]);
            document.write(v1);
            document.write(v2);
            return OK;
        }
        tag`Hello ${a+b} world ${a*b}`; 
        //输出结果为: "Hello "
        // "world "
        // 15
        // 50
        // "OK"
    ```
    
 7. String.raw () 方法
 
    模板字符串可以是原始的 ( 所谓的原始就是不会转义任何字符,任何字符都会以普通字符串的方式来输出 ), 若使用 String.raw 作为模板字符串的前缀, 则模板字符串可以是原始的, 反斜线也不再是特殊字符, \n 也不会被解析成换行符 ( 需要注意的是如果字符串里包含有html标签, 则会转义相对应的Dom元素 ), 例如:

    ```javascript
        let str = String.raw`Not a newline: \n<br/>Hello World`;
        document.write(str);
        //输出结果为: 'Not a newline:'
        // 'Hello World'
    ```
    


### (二) 数值

 1. 判断值是否为无穷或者NaN
    
    Number.isFinite ( ) 和 Number.isNaN ( ) 两个方法用来检查 Infinite 和 NaN 这两个特殊值, 例如: 
    
    Number.isFinite( ) 用来检查一个数值是否 非 无穷
    
    ```javascript
        // 判断是否
        Number.isFinite(15);                    // true
        Number.isFinite(0.8);                   // true
        Number.isFinite(NaN);                   // false
        Number.isFinite(Infinity);              // false
        Number.isFinite(-Infinity);             // false
        Number.isFinite("foo");                 // false
        Number.isFinite("15");                  // false
        Number.isFinite(true);                  // false
    ```
    
    Number.isNaN( ) 用来检查一个值是否为NaN
    
    ```javascript
        Number.isNaN(NaN);                  // true
        Number.isNaN(15);                   // false
        Number.isNaN("15");                 // false
        Number.isNaN(true);                 // false
    ```
    
 2. 值是否为整数
 
    Number.isInteger( ) 用来判断一个值是否为整数, 在javascript内部, 整数和浮点数是同样的储存方法, 所以 3 和 3.0 被视为同一个值, 例如: 

    ```javascript
        Number.isInteger(25)            // true
        Number.isInteger(25.0)          // true
        Number.isInteger(25.1)          // false
        Number.isInteger("15")          // false
        Number.isInteger(true)          // false
    ```
    
 3. Math 对象
 
    Math 对象新增的方法, 都是静态的方法, 只能在Math对象上调用.

    - Math.trunc( ) : 
      去除一个数的小数部分, 返回整数部分, 例如: 
    
      ```javascript
        Math.trunc(4.1);            //输出: 4
        Math.trunc(-4.1);           //输出: -4
        Math.trunc("23");           //输出: 23
        Math.trunc("23dsadsa");     //输出: NaN
        Math.trunc("");             //输出: 0
      ```
      
      注意: 对于空值和无法截取整数的值, 返回 NaN
      
    - Math.sign( ) : 
      判断一个数到底是正数, 负数, 还是0, 返回值有五种: 参数为正数, 返回+1; 参数为负数, 返回-1; 参数为0, 返回0; 参数为-0, 返回-0; 其他值, 返回NaN;
      
      ```javascript
        Math.sign(-5);                   // -1
        Math.sign(5);                    // +1
        Math.sign(0);                    // +0
        Math.sign(-0);                   // -0
        Math.sign('hubwiz');             // NaN
      ```
     
    - Math.cbrt( ) : 
    
      计算一个数的立方根, 例如: 
      
      ```javascript
        Math.cbrt(-1);                  // -1
        Math.cbrt(0);                   // 0
        Math.cbrt(2);                   // 1.2599210498948732
      ```
      
    - Math.fround( ) :
    
      返回一个数的单精度浮点数形式, 例如: 
      
      ```javascript
        Math.fround(0);                 // 0
        Math.fround(1.337);             // 1.3370000123977661
        Math.fround("asdasd");          // NaN
        Math.fround("1.264");           // 1.2640000581741333
      ```
      
    - Math.hypot( ) : 
    
      返回所有参数的平方和的平方根, 例如: 
      
      ```javascript
        Math.hypot(3, 4);               // 5
        Math.hypot(3, 4, 5);            // 7.0710678118654755
        Math.hypot();                   // 0
        Math.hypot(NaN);                // NaN
        Math.hypot(3, 4, 'foo');        // NaN
        Math.hypot(3, 4, '5');          // 7.0710678118654755
        Math.hypot(-3);                 // 3
      ```
      
      注意: 如果参数不是数值, Math.hypot方法会将其转为数值, 只要有一个参数无法转为数值, 就会返回NaN;

### (三) 数组

 1. 将两类对象转为真正的数组 ( Array.from )
 
    Array.from ( ) 方法用于将两类对象转为真正的数组: 类似数组的对象和可遍历的对象, 例如; 

    ```javascript
        var obj = {
            0: "yeah",
            "1": "haha",
            name: "Andraw",
            length: 4
        };
        var str = Array.from(obj);
        console.log(str);       //输出为: ["yeah", "haha", undefined, undefined];
    ```
    注意: 转为数组的时候, 必须带有length属性, 否则无法把对象或者字符串转化为数组, 即空数组 [ ];
    
    Array.from ( ) 还接收第二个参数, 作用类似数组的map的方法, 用来对每个元素进行处理, 也可传一个函数作为第二个参数, 例如: 
    
    ```javascript
        var str = "Andraw";
        var arr = Array.from(str, function(x){
            console.log(x);
        });
        // 输出为: ["A", "n", "d", "r", "a", "w"];
    ```
    Array.from()的一个应用是: 将字符串转为数组, 然后返回字符串的长度, 这样可以避免JavaScript将大于\uFFFF的Unicode字符(即汉字), 算作两个字符的bug.
    

 2. 将值转换为数组 ( Array.of )
 
    Array.of方法用于将一组值, 转换为数组, 例如: 

    ```javascript
        Array.of(3, 11, 8);             // 输出为: [3, 11, 8]
        Array.of(3);                    // 输出为: [3]
        Array.of(3).length;             // 输出为: 1
    ```
    
    Array.of( ) 这个方法的主要目的是, 弥补数组构造函数的缺陷, 因为在数组构造函数里会根据参数个数的不同导致Array( ) 的行为有差异, 例如:
    
    ```javascript
        Array();                        // 输出为: []
        Array(3);                       // 输出为: [undefined, undefined, undefined]
        Array(3, 11);                   // 输出为: [3, 11]
    ```
    
    上面代码说明, 对于数组的构造函数, 值有当参数个数不少于2个! ! !  Array( ) 才会返回由参数组成的新数组;
    

 3. 找出第一个符合条件的数组成员和位置 ( find和findIndex )
 
    - find 方法
    
      用于找出第一个符合条件的数组成员, 只要找到第一个符合条件的数组元素, 即返回该元素, 如果找不到符合的成员, 则返回 undefined, 例如:

      ```javascript
        var arr = [1, -5, -2, 3, 0].find(function(value, index, arr){
            return value<0;
        });
        console.log(arr);               // 输出为: -5
      ```
      
      find 中的回调函数的参数依次是: 当前的值, 当前的位置, 原数组;
      
    - findIndex 方法
    
      用法与 find 方法非常类似, 返回第一个符合条件的数组成员的位置, 如果所有成员都不符合条件, 则返回 -1 ,例如: 
      
      ```javascript
        var arr = [1, 5, 10, 15].findIndex(function(value, index, arr){
            return value > 9;
        });
        console.log(arr);               // 输出为: 2
      ```
      
      注意: ES5中的 indexOf 方法无法识别数组的NaN成员, 但是 findIndex 方法可以借助 Object.is 方法做到, 例如: 
      
      ```javascript
        [NaN].indexOf(NaN);                         // 输出为: -1
        [NaN].findIndex(function(value){
            return Object.is(NaN, value);           // 输出为: 0
        });
      ```
      
 4. 填充数组 ( fill )
 
    fill ( ) 使用给定值, 填充一个数组, 例如: 

    ```javascript
        var arr = ["a", "b", "c"].fill(7);  
        console.log(arr);                   // 输出为: [7, 7, 7];
        var str = new Array(3).fill(7);
        console.log(str);                   // 输出为: [7, 7, 7];
    ```
    
    fill ( ) 方法对于数组中已有的元素, 在填充的过程中, 会全部抹去;
    
    fill ( ) 方法还可以接收第二个和第三个参数, 用于指定填充的起始位置和结束位置, 例如: 
    
    ```javascript
        var arr = ["a", "b", "c"].fill(7, 1, 2);
        console.log(arr);                   // 输出为: ["a", 7, "c"]
    ```
    
 5. 三个新的遍历方法
 
    以下三个

    - entries (  ) : 
    
      对键值对的遍历