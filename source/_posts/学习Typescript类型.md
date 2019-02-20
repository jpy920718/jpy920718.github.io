---
title: 学习Typescript类型
date: 2019-01-27 22:37:39
tags: 
    - Typescript
---
### Typescript 数据类型
* boolean
* number
* string
* array
* null 和 undefined
* tuple
* enum
* any
* void
* nerver

#### boolean
```javascript
    // boolean
    let bool = true; // 错误

    let bool: boolean = true; //正确

```
#### number
```javascript
    //number
    let num = 321; // 错误

    let num: number = 321; // Right
```
#### string
```javascript
    //string
    let str = 'jpy'; // Fail

    let str:string = 'jpy'; // right
```

#### array ts中定义数组有三种种方式
```javascript
    //array
    let arr = [1,2,3,4,5];// fail

    //定义数组并且指定数组里的元素都是number类型
    //第一种
    let arr:number[]= [1,2,3,4]; //right
    //第二种
    let arr:Array<number> = [1,2,3,4];// right
    // 第三章
    let arr:any[] = [1,'32',true,34]; //right

```
<!--more-->
#### undefined 和 null
```javascript
    //undefined
    let num: number | undefined;
    console.log(num); //undefined
    num = 123;
    console.log(num); //123

    //null 一个元素可能是number 可能是null 可能是 undefined
    let num: number | null | undefined;

```

#### 元祖类型（tuple）属于数组的一种，定义一个数组里元素要么可以是number又可以是string这时候就可以用元祖类型,给数组中每一个元素指定类型。
```javascript
    // Tuple
    let arr:[number,string] = [1,'233']; //right
    let arr:[number,string] = [11, 33]; //fail
```

#### enum 枚举类型 通过使用自然语言中含义清楚的单词来表示它的每个值，这种方法叫做枚举方法，用这种方法定义的类型叫做枚举类型

写法：
```javascript
enum 枚举名{
    标识符[=整型常数],
    标识符[=整型常数],
    ...
    标识符[=整型常数],
}
```
```javascript
    // enum
    enum Type {
        success=1,
        error=-1,
    };
    let result:Type = Type.success
    console.log(result) // 1

    //
    enum Color{
        red,
        origin,
        blue
    }
    let c: Color = Color.blue;
    console.log(c); //2 如果标识符没有赋值，它的值就是下标
```

#### any 任意类型

```javascript
    let num: any = 123; //right
    num = '123'; //right
    num = true; //right
```

#### void 没有任何类型 一般用于定义方法没有返回值
```javascript
    // 方法没有返回任何类型
    function func():void{
        console.log(123);
    }

    // 下面是错误写法
    function func(): number{
        console.log(123);//fail
    }

    function fuc(): undefined{
        console.log(123);//fail
    }
```

#### nerver 从不会出现的值 是其他类型的子类型包括null和undefined; 一般不会使用。
```javascript
    //nerver
    let a:nerver;
    a = 123;// fail

    //正确
    a = (() => {
        throw new Error('错误')；
    })
```