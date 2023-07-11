
## 常用操作

```bash
# 查看分支
git branch
git branch -a
git branch -r
git branch -vv

# 新建分支
git branch -b <分支名>
git checkout -b <本地分支名> origin/<远程分支名>

# 切换分支
git branch <分支名>

# 删除分支
git branch -d <分支名>
```

## 操作

> 设置（属性）、切换、增删改查

### 设置

1. 设置默认的分支名称`master`（`git init`）
```shell
git config --global init.defaultBranch master
```
2. 设置别名/简写
```shell
git config --global alias.br "branch"
```

### 切换

```shell
git checkout <分支名>
```

### 查看

*表示当前分支，白色表示本地分支，红色表示远程分支
1. 查看所有分支

```shell
git branch
```
2. 查看本地分支
```shell
git branch -a
```
3. 查看远程分支
```shell
git branch -r
```
4. 查看本地分支和远程关联分支（追踪分支）
```shell
git branch -vv
```

### 新建

1. 新建本地分支
```shell
git branch -b <分支名>
```
2. 从远程分支拉取新分支（含3步：创建、切换、关联）
```shell
git checkout -b <本地分支名> origin/<远程分支名>
```
3. 基于历史提交创建新分支
```shell
git checkout -b <分支名> <commitID>
```

### 删除

1. 删除指定本地分支
```shell
git branch -d <分支名>
```

### 修改
1. 修改本地分支（当前分支） #重命名
```shell
git branch -m <分支名>
```
2. 修改本地分支（其他分支） #重命名
```shell
git branch -m <旧分支名> <新分支名>
```
3. 修改远程分支 #重命名
```shell
只能先删除后再重新推送
```

### 关联

1. 将本地分支与远程分支关联
```shell
git branch --set-upstream-to origin/<远程分支名>
```

## 其他

### 常用分支名

```txt
main/master
trunk
development
```
