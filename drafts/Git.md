

## 分支branch

设置默认的分支名称（git init）
git config --global init.defaultBranch master

修改分支名
git branch -m <name>

查看分支
git branch
git branch -a
git branch -r
查看本地分支和追踪分支
git branch -vv
*表示当前分支，白色表示本地分支，红色表示远程分支

## 新建分支
git branch -b <分支名>
从远程分支拉取（3步：创建、切换、关联）
git checkout -b <本地分支名> origin/<远程分支名>

切换分支
git branch <分支名>

删除分支
git branch -d <分支名>


main/master
trunk
development


Scalar
[Git 2.38发布，引入巨型仓库管理工具"Scalar"_程序员大咖的博客-CSDN博客](https://blog.csdn.net/Px01Ih8/article/details/127661912)


提交commit

规范/模板
[git commit 模板设置_git msg 模板定制_宋大人-专注的博客-CSDN博客](https://blog.csdn.net/songmingzhan/article/details/80935441)
[git commit模板 - 苍山落暮 - 博客园 (cnblogs.com)](https://www.cnblogs.com/tomtellyou/p/14028838.html)
[优雅的提交你的 Git Commit Message - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/34223150)


## 重命名mv
git mv 文件或文件夹
保留文件历史修改记录
git mv <src> <dst>

## 日志log
查看分支图

图形化显示

## 回滚

git reset

## 远程

git remote add

## 变基 rebase

## 推送 push

git push -u <本地分支名>:<远程分支名>

## 拉取 pull

### 拉取分支最新代码
git rebase <远程分支名>== git pull -r/--rebase <远程分支名>
优点：提交记录简洁
缺点：改变基底，无法获取最早分支信息


## 配置 config

git config --global -l

查看配置
cat .git/config

git config --global core.editor vim
git config --global apply.whitespace nowarn  忽略文件中的空格修改

## 提交 commit

git commit --amend 修改上次提交注释或追加到上次提交（不新增commit记录，但会变更commitID，本质：生成新的commit替换了上次的commit）
git commit --amend --no-edit
