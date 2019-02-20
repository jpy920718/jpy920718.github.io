---
title: 学习Typescript函数
date: 2019-01-27 23:27:08
tags:
    - Typescript
---

## 函数定义 

### 指定返回类型
```js
//1函数声明法
    function fun():string{
        return 'run';
    }
//2匿名函数法
    let fun = function():string{
        return '123'
    }
// 没有返回值

    function fun():void{
        console.log('123');
    }
/*-----------*/
// 定义方法传参
    function fun(name:string, age: number): string{
        return `${name}---${age}`;
    }
    fun('jpy', 27); //right
    fun('jpy', '27'); //fail

    let getInfo = function(name: string,age:number):string{
        return `${name}---${age}`
    }

```
### ts中实参和形参必须一样，如果不一样需要配置可选参数,形参后面通过？来决定蚕食是否必传，如果有？则为可选参数，如果没有必传。
> 注：可选参数必须配置到参数的最后面

```js
    function getInfo(name: string, age?: number): string{
        if(age){
            return `${name}---${age}`
        }else{
            return `${name}`
        }
    }
    getInfo('jpy', 12);
    getInfo('jpy');
```
<!--more-->
### ts 默认参数，在es5中是无法设置默认参数的，es6之后和ts中可以设置默认参数

```js
    function getInfo(name: string, number=20):string{
        return `${name}---${age}`
    }
    getInfo('jpy');
    getInfo('jpy', 32)
```

### 剩余参数
```js
    // ...三点运算符
    function sum(...result: number[]): number{
        let sum = 0 ;
        result.map(item => sum+=item)
        return sum;
    }
    sum(1,2,3) //6
    //或者
    function sum(a: number, ...result: number[]): number{
        let sum = a ;
        result.map(item => sum+=item)
        return sum;
    }
    sum(1,2,3)//6
```

### ts函数重载 。
Java中函数重载，两个或者以上的函数名相同，但参数不同的函数叫做重载；typescript为了兼容es5以及es6重载的写法和java有区别。 在es5中出现同名的方法，后面的会替换前面的方法。ts中的重载，同样的方法，传入不同参数，执行不同的功能
```js
function getInfo(name: string):string;
function getInfo(age:number):number
function getInfo(str:any):any{
    if(typeof str === 'string'){
        return `名字：${str}`;
    } else if(typeof str === 'number'){
        return `年龄：${str}`;
    } else {
        throw new Error('类型错误')
    }
}
getInfo('jpy');//right
getInfo(18);//right
getInfo(true);//fail


```
> 以上ts代码经过编译后会变成如下

```js
function getInfo(str){
    if(typeof str === 'string'){
        return `名字：${str}`;
    } else if(typeof str === 'number'){
        return `年龄：${str}`;
    } else {
        throw new Error('类型错误')
    }
}
```


### 箭头函数 this指向上下文

```js
setTimeout(()=>{
    console.log(111);
})
```