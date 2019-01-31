---
title: 学学小程序之--小程序模板及include和import的区别
date: 2019-01-22 22:26:26
tags: 小程序
---


### 小程序中模板的定义

name 模板的名称
is声明使用哪个模板，通过data向模板传入信息，只能通过data传入
```bash
// index.wxml
<template name="tempItem">
    <view>
        <view>收件人：{{name}}</view>
        <view>联系方式：{{phone}}</view>
        <view>地址：{{address}}</view>
    </view>
</template>
<template is="tempItem" data="{{...info}}"></template>
//index.js
Page({
    data: {
        info: {
            name: '张三',
            phone:'123232323',
            address: '中国'
        }
    }
})
```
### 小程序模板引用include和include


#### inport只会引用template内的的内容，动态的传入数据，is表示引用的模板名称，data表示传入模板的数据, 不要死循环应用模板
```bash
    // index.wxml
    <import src="a.wxml"></import>
    <template is="a"></template>
    // a.wxml
    <view>
        a里的helloword
    </view>
    <template name="a">a的模板里的helloword！！ </template>
```
#### include只会引用除template内容外的内容

```bash
    //index.wxml
    <include src="a.wxml"></include>
    <template is="a"></template>

    //a.wxml
    <template name='a'>
        <view>模板内容</view>
    </template>
    <view>
        模板外的内容
    </view>
```
