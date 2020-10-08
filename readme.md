git reset HEAD 文件名： 将文件从暂存区变成非暂存区
git checkout -- 文件名： 将非暂存区的文件的修改丢弃（对于删除文件也有用）

git remote -v    查看远端仓库的分支
git remote add 远端仓库的别名  <url>   新建一个远端仓库
git remote rm 远端仓库的别名           删除一个远端仓库
git remote rename origin_ssl origin    将origin_ssl 改名为origin
git remote show origin   可以查看push到origin远端的那个分支

git log -p -1 查看最近一次提交的差异，也可以使用git log -p 查看所有的差异
git log --stat	查看简化版的diff日志信息。只会给出某个文件增加或减少的某个代码量，而不会给出详细的修改内容
git log --pretty=oneline 或者 git log --oneline 每次的commit在一行上显示