---
title: 学习Typescript类
date: 2019-01-29 23:40:42
tags:
    - typescript
---

# es5的类

### es5中定义一个简单的类
```js
    function Person(){
        this.name='jpy';
        this.age=18;
    }
    let person = new Person();
    console.log(person.name);
```
### 构造函数和原型链中增加方法

```js
    function Person(){
        this.name='jpy';
        this.age=18;
        this.run = function(){
            console.log(`${this.name}在走路`)
        }
    }
    let person = new Person();
    person.run();// jpy在走路


    // 在原型链上定义属性和方法，
    Person.prototype.sex = '男';
    Person.prototype.work = function(){
        console.log(`${this.name}在工作`)
    }
    person.work();// jpy在工作
```
原型链上的属性和方法会被多个实例共享但是构造函数不会

### 类中的静态方法
```js
    function Person(){
        this.name='jpy';
        this.age=18;

    }
    Person.getInfo = function(){
        return `姓名：${Person.name}`
    }
    Person.getInfo();//姓名：jpy
```

### 继承 原型链+对象冒充的组合继承模式.
#### 对象冒充继承可以继承Person构造函数里面的属性和方法，但是不能继承Person原型链上的属性和方法
#### 原型链继承可以继承Person的构造函数的属性和方法，也能继承原型链上的方法，但是实例化子类时无法给父类传参。
```js
    function Web(){
        Person.call(this);//对象冒充实现继承

    }

    var w = new Web()
    w.run();//可以继承Person里面的属性和方法，但是不能继承Person原型链上的属性和方法
    w.work();// console.error(

    
```
```js
    function Web(){
        Person.call(this);//对象冒充实现继承

    }
// 原型链实现继承
    web.prototype = new Person();
    w.run();//ok
    w.work();//ok
```

### 原型链+构造函数的组合继承

```js
    function Web(){
        Person.call(this, name, age); //对象冒充可以继承Person构造函数里面的属性和方法，但是不能继承Person原型链上的属性和方法
    }
    Web.prototype = new Person();
    var w = new Web('张三', 22);
```

#### 另一种写法 直接继承父类的原型链
```js
     function Web(){
        Person.call(this, name, age); //对象冒充可以继承Person构造函数里面的属性和方法，但是不能继承Person原型链上的属性和方法
    }
    Web.prototype = Person.prototype;
    var w = new Web('张三', 22);
    w.run();
```


# ts中类 

### 通过class 关键字来定义
```js
class Person{
    name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): void{
        console.log(`${this.name}在跑步`)
        }
}

var p = new Person('张三')；
p.run();
```


```js
    class Person{
    name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): void{
        console.log(`${this.name}在跑步`)
        }

    getName():string{
        return this.name;
    }
    setName(name:string):void{
        this.name = name
    }
}

var p = new Person('张三')；
p.getName(); // '张三'


p.setName('李四')；
p.getName();//‘李四’
```

### ts中实现继承 通过extends、super
```js
     class Person{
    name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}

let p = new Person('王五')
p.run();//王五在跑步

//开始实现继承, 在构造函数里使用super

class Web extends Person{
    |constructor(name：string){
        super(name);//初始化父类的构造函数
    }
}

let w = new Web('李四')
w.run();//李四在跑步
```

### ts中继承的探讨
```js
//父类
class Person{
    name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
//子类
class Web extends Person{
    |constructor(name：string){
        super(name);//初始化父类的构造函数
    }
    run(): string{
        return `${this.name}在跑步--子类`
    }
    work():string{
        return `${this.name}在工作--子类`
    }
}

let w = new Web('李四')；
w.run();//李四在跑步--子类
w.work();//李四在工作--子类
```
> 当子类中的方法与父类的方法相同时执行子类的方法

# ts类里的修饰符，在typescript 里定义属性时有三总修饰符 public protected private

### public：公有   在类里面、  子类里、 类外面都可以访问
#### 类里面访问公有属性
```js

class Person{
    public name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
var p = new Person('张三')；
p.run();//张三在跑步
```
#### 子类中访问公有属性
```js
class Person{
    public name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
class Web extends Person{
    constructor(name:string){
        super(name)
    }
    work(): string{
        return `${this.name}在工作`
    }
}

let w = new Web('李四');
w.work();// 李四在工作
```
#### 在类外面访问公有属性
```js
class Person{
    public name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}

let p = new Person('哈哈');
console.log(p.name); //哈哈

```
### protected: 保护类   在类里面可以方位、 子类里面可以访问，但是在类外面是不可以访问的
#### 类里面访问保护protected属性
```js

class Person{
    protected name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
var p = new Person('张三')；
p.run();//张三在跑步
```
#### 子类中访问保护protected属性
```js
class Person{
    protected name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
class Web extends Person{
    constructor(name:string){
        super(name)
    }
    work(): string{
        return `${this.name}在工作`
    }
}

let w = new Web('李四');
w.work();// 李四在工作
```
#### 在类外面访问保护protected属性
```js
class Person{
    protected name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}

let p = new Person('哈哈');
console.log(p.name); //error，编译为es5没有问题但在ts中是错误的

```

### private:私有类 在类里面可以访问，但是在子类、类外面是不可以访问的
#### 类里面访问私有private属性
```js

class Person{
    private name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
var p = new Person('张三')；
p.run();//张三在跑步
```
#### 子类中访问私有private属性
```js
class Person{
    private name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}
class Web extends Person{
    constructor(name:string){
        super(name)
    }
    work(): string{
        return `${this.name}在工作`
    }
}

let w = new Web('李四');
w.work();// error 编译为es5没有问题但在ts中是错误的
```
#### 在类外面访问私有private属性
```js
class Person{
    private name: string; //属性， 省略了public关键词
    constructor(name: string){ //构造函数  实例化类的时候触发的方法
        this.name = name;
    }
    run(): string{
        return `${this.name}在跑步`
    }

}

let p = new Person('哈哈');
console.log(p.name); //error，编译为es5没有问题但在ts中是错误的

```


#### 定义属性时未加修饰符时，默认为public
