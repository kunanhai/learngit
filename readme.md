## 克隆项目
1. git clone url  执行后会在本地目录下新建一个目录，所以不用新建一个目录的。
2. 执行git init
3. 此时只有一个master分支，一般还需要别的分支，比如dev开发分支等，在另外一个分支上工作，如果你希望将远程仓库的dev分支也克隆下来，则执行 git checkout -b dev origin/dev
接下来就可以在本地工作了 

新建分支的步骤可以分成两个：
git branch hello    创建hello 分支
git checkout hello  跳转到hello分支

##　将本地项目上传到github
1. git init
git init的作用是初始化git本地仓库。
git add .
git commit . -m "message"
到这里本地仓库已经有你的修改记录了
2. git remote add origin url 将远程仓库连接到本地仓库
origin是你远端仓库的名称，github上一般都是origin。 url是远端仓库的地址，复制即可。
3. git push -u origin master    将本地库master分支上修改的内容推送到github的远程仓库master分支上面(-u 是--set-upstream的简写)，第一次需要这样做，下次再推送的时候直接执行git push origin master就可以了（但前提是上一步必须加-u)
（注意： 如果远程库上没有建立master分支，一般发生在第一次提交新分支的时候，github会主动创建分支）

## 创建分支： 
1. git branch note  //创建note分支
2. git checkout note //切换到该分支
3. git checkout -b note //创建并切换到该分支
4. 把分支添加到上
git push --set-upstream origin note //将note分支上传到github上

## 删除上github上某个分支的文件夹
在github上只能删除仓库，不能删除目录，只能通过本地解决。如：删除master分支下的doc目录
1. git pull origin master //将远程仓库里面的master分支的项目拉下来（前提是要先git remote add一下，不然不知道是那个仓）
2. dir //查看master分支有哪些文件夹
3. git rm -rf --cached doc //删除
4. git commit -m "delete doc"
5. git push origin master //推送本次更改

## 如何把dev分支的修改合并到主干分支（main）上
1. 现在dev分支上做提交，并git push后
2. 本地切换到main分支， git merge dev
3. 本地main分支已经带上修改了，这个时候再git add, commit, push一下
## 常用的git回撤操作
1. commit回滚
   git reset --soft HEAD^ ： --soft保持之前的修改不被丢弃，（不要用--hard, 修改会被直接丢弃), HEAD^ 等于HEAD~1, 表示回滚到上个版本
2. 本地仓撤销操作
git reset HEAD 文件名： 将文件从暂存区变成非暂存区
git checkout -- 文件名： 将非暂存区的文件的修改丢弃（对于删除文件也有用）

## 远程仓库操作
git remote -v    查看远端仓库的分支
git remote add 远端仓库的别名  <url>   (新建一个远端仓库)
git remote rm 远端仓库的别名           (删除一个远端仓库)
git remote rename origin_ssl origin    将origin_ssl 改名为origin
git remote show origin   可以查看push到origin远端的那个分支

git log -p -1 查看最近一次提交的差异，也可以使用git log -p 查看所有的差异
git log --stat	查看简化版的diff日志信息。只会给出某个文件增加或减少的某个代码量，而不会给出详细的修改内容

## 同步远程仓库解决冲突
1. git pull origin master   // 同步远程仓库主干，这时候别人如果对相同文件做了修改，需要解决冲突
2. git status 查看那些文件需要解决冲突
3. vim 文件修改
4. git add 文件（不需要commit，只是解决冲突）
5. git pull 就可以了

或者使用git stash 先将本地的修改暂存起来，git pull 之后再 git stash pop 一下。


## 别名使用，提高效率
git config --global alias.别名  要替换的名字：
如: git config --global  alias.st  status
	git config --global  alias.co  checkout
	git config --global  alias.last log -1 HEAD
	
通过git config -l可以查看你设置过的所有别名

## 常见问题
1. git remote add origin url 命令解析
url 是线上库的地址，origin为线上仓的别名，后面的git push origin master 代表将master分支的内容push到线上origin仓上

2. OpenSSL问题，有时候是网络卡顿的原因，github国内网速有点慢，解决方法是 git config --global http.sslVerity "false"

3. refuse to merge unrelated histories. 原因不清楚，感觉是两个仓是独立导致的。解决办法是merge分支的时候加上 --allow-unrelated-histories
