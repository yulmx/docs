
## 参考

[Git - Git 别名 (git-scm.com)](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-Git-%E5%88%AB%E5%90%8D)

## 设置

### 1. 编辑配置文件`~/.gitconfig`

```ini
[alias]  
st = status  
ci = commit  
br = branch  
co = checkout  
df = diff  
ss = stash  
ssp = stash pop
```

### 2. 使用命令行添加

```shell
git config --global alias.p 'push'
git config --global alias.d 'diff'
```

## 操作

### 查看

```shell
git config --global -l
```

## 常用别名

1. 查看已更改或未跟踪的文件，并简化输出
```shell
git config --global alias.st 'status -sb'

git st
```
2. 单行显示提交日志
```shell
git config --global alias.ll 'log --oneline'

git ll
```
3. 最新一次提交详情
```shell
git config --global alias.last 'log -1 HEAD --stat'

git last
```
4. 提交
```shell
git config --global alias.cm 'commit -m'

git cm "comments"
```
5. 查看所有远程仓库
```shell
git config --global alias.rv 'remote -v'

git rv
```
6. 指定显示特定文件两次提交内容差异
```shell
git config --global alias.dv 'difftool -t vimdiff -y'

git dv 33559c5 ca1494d file1
```
7. 查看你所有配置
```shell
git config --global alias.gl 'config --global -l'

git gl
```
8. 搜索提交
```shell
git config --global alias.se '!git rev-list --all | xargs git grep -F'

git se <keyword>
```

## 别名列表

```
st = status  
ci = commit  
br = branch  
co = checkout  
df = diff  
ss = stash  
ssp = stash pop

```




