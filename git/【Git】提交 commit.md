---
aliases: 【Git】提交 commit
tags: #Git #doc #template
date: 20230709 20:43:20
---

## 常用操作

1. 提交
```shell
git commit -m "注释"
```
2. 追加到最近提交（并修改注释）或仅修改commit注释
```shell
git commit --amend
```
3. 追加到指定历史提交（并修改注释）
```shell
# 1. 暂存待提交修改内容
git stash
# 2. 验证是否stash成功（可选）
git stash list
# 3. 查看指定commit的id并复制
git log
# 4. 变基并进入vim（以指定commit的上一提交为基底）
git rebase -i <commitID>^
# 5. 修改pick（p）成edit（e）并保存退出
# 6. 取出修改内容并手动解决冲突
git stash pop
# 7. 添加并提交
git add . && git commit --amend
# 8. 回退到最新，即变基到最新commit
git rebase --continue
# 9. 强推到远程
git push -f
```
4. 提交后撤销（保留修改）
```shell
git reset --soft HEAD^
```
5. 提交后撤销（不保留修改）
```shell
git reset --hard HEAD^
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

```shell

```

### 新建

```shell

```

### 删除

```shell

```

### 修改

1. 修改上一次commit即最近一次commit
```shell

```
2. 修改指定历史提交
```shell

```
## 其他

### 1. 添加commit模板

1. 在用户家目录添加文件`.gitcommittemplate`

```txt
问题: 
原因: 
解决方案: 
作者: 
日期: 
```
2. 修改git配置文件
```shell
git config --global commit.template ~/.gitcommittemplate
```