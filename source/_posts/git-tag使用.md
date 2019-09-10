---
title: git - tag 使用
date: 2019-09-09 00:34:18
tags:
    - git
---

### 更改内容提交
```bash
    git add .
    git commit -m '提交1'

    git tag tag_01

```
### 回退修改前版本
```bash
    git reset --hard xxxx // xxxx 提交hashid
```

### 修改内容提交
```bash
    git add .
    git commit -m '提交1'

    git tag tag_02

```

### 使用git tags 查看tag list
```bash
    git tags

```

### 将tags push至远程
```bash
    git push --tags
```




