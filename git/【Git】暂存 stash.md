---
aliases: 【Git】暂存 stash
tags: #Git #doc #template
date: 20230709 20:03:03
---

## 常用操作

1. 暂存所有代码（已被git跟追）
```shell
git stash
```

## 操作

> 设置（属性）、切换、增删改查

### 设置

1. 设置
```shell

```
2. 设置别名/简写
```shell
git config --global alias. ""
```

### 查看

1. 查看所有暂存列表（git栈）
```shell
git stash list
```

> 1. stash@{index}：倒数第index笔暂存

### 添加 push

1. 添加所有（等价）
```shell
git stash
git stash push .
```
2. 添加暂存并备注
```shell
git stash save "comments"
```

### 取出 pop

1. 取出最新（并从栈中删除）
```shell
git stash pop
git stash pop stash@{index}
```
2. 取出指定（并从栈中删除）
```shell
git stash pop stash@{index}
```
3. 取出但不删除（即仅应用）
```shell
git stash apply stash@{index}
```

### 删除

1. 清空stash栈
```shell
git stash clear
```
2. 删除指定stash
```shell
git stash drop stash@{index}
```

## 其他

1. 查看暂存文件内容
```shell
git stash show -p stash@{index}
```
