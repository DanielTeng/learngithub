## 获得版本库

+ git init
+ git clone

## 版本管理

+ git add
+ git add . (通配符)
+ git commit -m ""
+ git commit --amend -m "修改上次提交的备注"
+ git rm (git rm --cached <\file>)
+ git rm test.txt (完成2步，1，删除；2，文件放入暂存区;自动做了纳入暂存区)
+ git reset HEAD <\file>(从暂存区恢复到工作区,恢复2)
+ git checkout --test.txt (撤回删除，撤回1)
+ rm test.txt (仅仅完成1步，1，删除；还需要git add test.txt来放入暂存区)

## 查看信息

+ git help
+ git log
+ git log -5 （只查最近5条提交信息）
+ git log --pretty=oneline
+ git log --pretty=format:"%h -%an, %ar :%s"
+ git log --graph 图示git log
+ git dif
+ git status (当前git状态)

## 远程协作

+ git push
+ git pull

## 配置操作

+ git config (git config --global user.name "Your Name")
+ git config (git config --global user.email "Your Email")
+ git config --global --replace-all user.name "Daniel_Teng"
+ git config --global --replace-all user.email "tengyong1971@gmail.com"
+ git config --list
+ system -> global -> local 系统 -> 用户 -> 项目
+ git config --global color.ui auto
+ git help config
+ git config --help
+ man git-config (这需要linux系统)

## 撤销工作区操作

+ git checkout -- test.txt

## 文件重命名

+ git mv test.txt test1.txt (move)

## .gitignore 忽略

+ .gitignore是一个文件，本身受git管理
+ 进入.gitignore的文件名，不受git管理
+ build/加入.gitignore;忽略build目录下所有文件。

## 分支

+ git branch 显示当前所有分支
+ git branch new_branch 创建新分支
+ git checkout new_branch 切换到新分支
+ git branch -d new_branch 删除分支(假如并无新文件)
+ git branch -D new_branch 强制删除分支
+ git checkout -b new_branch2 创建并切换到新分支
+ git branch -m branch_old_name branch_new_name 修改分支的名字
+ git merge new_branch2 合并分支，是默认的fast forward模式
+ git branch -v 本分支最近的变动
+ git merge --no-ff new_branch 合并分支，不用ff模式，新建一个提交commit

## 分支的本质和master的本质

+ HEAD是分支branch的pointer，指向master
+ master是提交commit的pointer，指向最新的提交
+ 新建的new_branch跟master一样，指向同一个最新的提交
+ 真是指针的妙用

## git的版本回退

+ git reset --hard HEAD^ 回退上一个版本(windows的cmd控制台把^做为换行符，所以问more？)
+ git reset --hard HEAD~1 回退1个版本
+ git reset --hard commit_id 回退特定版本，可进
+ git reflog 操作记录，用于向前回退的查找commit_id

## checkout进阶

+ git checkout -- filename 撤销对工作区working file文件的变更,指尚未add到暂存区的变更
+ git reset HEAD filename 暂存区文件撤回到工作区状态
+ git checkout commit_id (HEAD detached, 游离状态，to look around, 跟git reset --hard commit_id不同)
+ git commit -am "" 游离状态下的提交，是孤立的commit提交，不在任何分支branch上，无法追踪，如下
+ git branch new_branch_name commit_id 为如上的孤立commit创建一个新的分支，这跟merge无关,可追踪

## 分支工作的stash（工作区现场保存）

+ git stash 保存工作区现场：工作的临时保存，建立WIP（working in process）索引，可以checkout了
+ git stash list 列举工作区现场，临时保存的列表
+ git stash pop 最常用，重回工作区现场，重回工作区工作状态(取回临时状态，恢复，并删除原WIP)
+ git stash apply 重回工作区现场，工作区工作状态(取回临时状态，恢复，但并不删除原WIP)
+ git stash drop stash@{n} 手动删除工作区现场
+ git stash apply stash@{n} 指定工作区现场版本，恢复

## 标签

+ 2种标签: 标签不属于分支。用于发布，里程碑。
+ 轻量级标签：lightweight；git tag v1.0.1
+ 带有附注的标签：annotated; git tag -a v1.0.2 -m "released version"
+ 删除标签：git tag -d tag_name
+ 查看标签：git tag
+ 查找标签：git tag -l "v1.0"

## git blame

+ git blame : 添加环境变量：LESSCHARSET=utf-8;解决git cmd中文乱码问题。
+ git blame filename: 每一行。最后的修改时间，修改人。

## diff

+ 4种差别
+ 1: 工作区跟暂存区（索引区）的文件差别。git dif, 暂存区是原始文件（源）-，工作区是目标文件+。
+ 2: 工作目录与某一提交的差别。
+ 3: 暂存区与某一提交的差别。
+ 4: 比较两个提交之间的差别。
