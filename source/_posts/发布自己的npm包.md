---
title: 发布自己的npm包
date: 2019-05-12 17:52:57
tags:
    - npm
---

### 1. [npmjs.com](https://npmjs.com) 注册账号

### 2. 初始化项目

```bash
   $ mkdir jpy-test-package
   $ cd jpy-test-package
   $ npm init
```
### 3. 代码
```js
    function jpyPackageDemo () {
        console.log('test first npm package!');
    }

    module.exports = jpyPackageDemo();
```

### 4. 发布
```bash
    $ npm login

    ...

    $ npm publish
```

### 5. 更新
- 更改源代码
```js
    function jpyPackageDemo () {
        console.log('test first npm update package!');
    }

    module.exports = jpyPackageDemo();
```
- 更新至npm
> npm version <type> : patch, minor,  major(补丁，小改，大改)
```bash
    npm version minor
    npm publish
```
### [参考](https://www.cnblogs.com/penghuwan/p/6973702.html#_label3_0)
