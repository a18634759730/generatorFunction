  
# generator(生成器) 

> ES6标准引入的新的数据类型，看上去是一个函数但是他可以返回多次

> 函数在执行过程中，如果没有遇到return语句 函数末尾如果没有return，就是隐含的"return undefined"，控制权无法交回被调用的代码

> generator 与 函数不同的就是 他是有 function* 定义的，并且除了return语句，还可以用 yebid 放回多次

> 函数只能放回一次，所以必须返回是Array,但是如果是generator就可以一个次返回一个数，不断返回多次

## 要编写一个产生斐波那契数列

> 函数方式

    function fib(max) {
        var t,
            a = 0,
            b = 1,
            arr = [0, 1];
        while (arr.length < max) {
            [a, b] = [b, a + b];
            arr.push(b);
        }
        return arr;
    }
    fib(5); // [0, 1, 1, 2, 3]
    fib(10); // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
    
> generator方式

    function* fib(max) {
        var t,
            a = 0,
            b = 1,
            n = 0;
        while (n < max) {
            yield a;
            [a, b] = [b, a + b];
            n ++;
        }
        return;
    }
    fib(5)//直接调用一个generator和调用函数不一样 fib(5)仅仅是创建了一个generator对象，还没有去执行它
   
    var f = fib(5)
    f.next() {value: 1,done: false}
    f.next() {value: 2,done: false}
    f.next() {value: 3,done: false}
    f.next() {value: 4,done: false}
    f.next() {value: 5,done: false}   
    f.next() {value: undefined ,done: true}

## 调用generator函数有个两个方法

> 1.不停的调用generator对象next()方法

        next()方法会执行generator的代码，然后，每次遇到yield x;
    就返回一个对象{value: x, done: true/false}，然后暂停,返回的
    value就是yield的返回值，done表示这个generator是否已经执行结
    束了。如果done为true，则value就是return的返回值
        当执行到done为true时,这个generator对象就已经全部执行完毕，
    不要再继续调用next()了

        补充:next()函数返回一个对象,value表示yield后表达式的值，
    done表示函数的执行状态,
        下一次next()调用传入的值是上一次调用的放回值
  
> 2.for ... of

    for of循环迭代generator对象,这种方式不需要我们自己判断done
