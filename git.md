## 获得版本库

+ git init
+ git clone
+ git --version 查询当前git版本
+ rm -rf .git 删除git本地仓库

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
+ git log 提交日志
+ git reflog 操作日志，也很有用，凡是修改HEAD指向的操作都被记录，据此跟踪commit的sha1值。
+ git log -5 （只查最近5条提交信息）
+ git log --pretty=oneline
+ git log --pretty=format:"%h -%an, %ar :%s"
+ git log --graph 图示git log
+ git diff
+ git status (当前git状态)

## 远程协作

+ git push
+ git pull == fetch + merge

## 配置操作

+ git config (git config --global user.name "Your Name")
+ git config (git config --global user.email "Your Email")
+ git config --global --replace-all user.name "Daniel_Teng"
+ git config --global --replace-all user.email "419885411@qq.com"
+ git config --list
+ system -> global -> local 系统 -> 用户 -> 项目
+ git config --global color.ui auto
+ git help config
+ git config --help
+ man git-config (这需要linux系统)
+ git config --global credential.helper store (git远程记住用户名和密码）
+ git config --global alias.br branch （设置别名）
+ git config --global alias.ui !gitk (为外部命令设置别名)

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
+ 1: 暂存区（索引区）跟工作区的文件差别。git diff, 暂存区是原始文件（源）-，工作区是目标文件+。
+ 2: 某一提交与工作区的差别。git diff commit_id, git diff HEAD（最近的提交）,版本库是源，工作区是目标。
+ 3: 某一提交与暂存区的差别。版本库是源，暂存区是目标。git diff --cached
+ 4: 比较两个提交之间的差别。git diff commit_id1 commit_id2 filename (第一个是源，第二个是目标)

## 远程git，github

+ github 与 gitlab
+ github账号注册和登录
+ 在github新建repository，取名learngithub
+ git remote add origin https://github.com/DanielTeng/learngithub.git 添加远程库(origin = https://github.com/DanielTeng/learngithub.git)
+ git push -u origin master (-u,把本地master跟远程master关联)（The key is "argument-less git-pull".）… is the same as:git push origin master ; git branch --set-upstream master origin/master
+ git push 直接推送(在已经关联远程库以后)
+ git remote show (列出所有与本地本仓库对应关联的远程仓库的别名,代替http资源地址)
+ git remote show origin (远程仓库的详细信息)
+ git remote add 命令会自动生成refspec, git会获取远端refs/heads下所有引用,写在本地refs/remotes/origin目录下.如下
+ fetch = +refs/heads/*:refs/remotes/origin/* (+ 是调取git fetch一定成功，merge不一定成功,允许fast forward)
+ git log origin/master 查看远端master分支的提交历史
+ 等价命令 git log remotes/origin/master; git log refs/remotes/origin/master,最完整)

## gitflow 工作流程

+ master 主分支(非常稳定)
+ hotfix(n) 紧急修复 (临时)
+ release(n) 发布 (稳定)(略，跟test重复)
+ test(n) 测试（更新不是很频繁)
+ develop 开发 （频繁更新）
+ feature(n) 功能开发 (分工，日常)

## 如何在仓库的settings 部署 keys（公钥）

+ 总是可读，勾选可写
+ 可以部署多个公钥
+ 针对特定仓库

## git远程协作

+ 当A落后于远程仓库，无法push，要先pull,这会有merge(假如有冲突，需要A进行人工merge解决冲突)。然后push。
+ 远程库只是交互交换中心。
+ 本地会有1个origin/master分支。是远程master分支的索引或引用吗？(实现了比对远程的本地化)(无法修改，是只读的，git系统自动维护。)
+ git branch -a 能查看到远程分支的索引。(remotes/origin/master)这个remotes说明这个分支也在本地，指向remotes。
+ git branch -av 包括了分支的最近一次提交。能看出本地分支和关联远程分支的进度关系。
+ git clone: 把远程仓库获取到本地。另一用户，另一机器，另一文件夹。远程库名成为下级文件夹。
+ git clone https://github.com/DanielTeng/learngithub.git
+ git clone https://github.com/DanielTeng/learngithub.git mygit2 (这就不用远程库名learngithub做默认文件夹了，用mygit2)
+ (git config --local user.name "luzhiqian") (git config --local user.email "tengyong1971@gmail.com") 设置
+ (git config user.name) (git config user.email) 查看
+ (在mygit2目录执行git branch -av,另外可以看到 remotes/origin/HEAD -> origin/master)??
+ git pull 是合并执行git fetch(取回到origin/master); git merge origin/master(与更新的origin/master做merge).

## gitk, git gui 图形界面工具

+ gitk (tcl/tk)
+ git gui
+ github desktop

## 分支改名

+ git branch -m original_branch_name new_branch_name (不在本分支)
+ git branch -m new_branch_name (在本分支)
+ 重命名远程分支，只能删了重建

## 本地分支到远程分支的建立，本地分支从远程分支建立 refspec的概念

+ git push --set-upstream origin develop (推送并在远程建立关联新分支)
+ git push --set-upstream origin develop:develop2 (推送并在远程建立关联新分支,不同名，不要用)
+ git push origin HEAD:develop2 (不同名的分支的上推，不要用，这个HEAD是指当前本地分支)
+ git pull (先取回新分支，但本地无新分支)
+ git checkout -b develop origin/develop (基于远程分支建立本地新分支，这个远程分支是个ref)
+ git checkout --track origin/develop (新版本的写法)

## 删除本地分支 删除远程分支

+ git branch -d branch_name (删除本地分支)
+ git push 的完整写法：git push origin src:dest (本地分支的名字：远程分支的名字，2个名字可以是不同的)
+ git pull 的完整写法：git pull origin remote_src:local_dest
+ git push origin  :dest (推空分支到远程，删除远程分支)
+ git push origin --delete remote_branch_name (新版版本删除远程分支，更好理解)

## 底层命令

+ symbolic-ref 底层命令，实现对HEAD文件的修改，HEAD，是指向指针的指针，commit实质的变化，会导致指针和指针的指针的变化。
+ git symbolic-ref (HEAD refs/heads/master) 底层命令并不会被reflog记录。

## 标签的远程

+ git tag (列举，tag，静态，关联特定commit_id,实现迅速查找特定commit)
+ git tag show v1.0 (commit操作的文件变化都能显示)
+ git tag -l "?2*" 使用正则对标签做搜索
+ git push origin v1.0 推送标签到远程
+ git push origin v2.0 v3.0 一次推送2个标签
+ git push origin --tags 推送全部未被推送的标签
+ git tag, github对应的是release
+ git push origin :refs/tags/v2.0 删除远程标签 (refspec)
+ git push origin --delete tag v2.0 删除远程标签
+ 标签推送的完整写法 git push origin refs/tags/v7.0:refs/tags/v7.0
+ 拉取特定标签 git fetch origin tag v7.0
+ 另一个人删除了远程develop分支，显示refs/remotes/origin/develop stale (use 'git memote prune' to remove)
+ git remote prune origin (剪掉过期的远程分支ref) (git remote show origin,信息干净)
+ git checkout v1.0 (切换到标签上，commit游离状态)

## git gc

+ git gc 暂不用，packed-refs

## git裸库

+ 没有工作区， git init --bare

## submodule

+ 项目依赖
+ parent项目，child项目
+ git remote add origin https://github.com/DanielTeng/git_parent.git
+ git remote add origin https://github.com/DanielTeng/git_child.git
+ git submodule add https://github.com/DanielTeng/git_child.git mymodule (mymodule是不存在的本地目录，会新建，原有的话会报错)
+ 会克隆submodule，需要加入暂存,提交和push。关联了2个库。
+ 当submodule更新，cd mymodule; git pull.拉取更新。
+ 更新全部submodule；在项目根目录，git submodule foreach git pull
+ 当新人加入git_parent; git clone https://github.com/DanielTeng/git_parent.git git_parent2
+ submodule关系会自动克隆下来，但内容不会。需要手动做：
+ 1，git submodule init;注册submodule；
+ 2，git submodule foreach git pull;更新。(git submodule update --recursive)
+ 递归的克隆，把子模块也克隆下来。git clone https://github.com/DanielTeng/git_parent.git git_parent3 --recursive
+ 移除submodule:1,从暂存区删除，2，从工作区删除，3，删除.modules目录。
+ 1,逆初始化模块，其中{MOD_NAME}为模块目录，执行后可发现模块目录被清空 git submodule deinit {MOD_NAME}
+ 2,删除.gitmodules中记录的模块信息（--cached选项清除.git/modules中的缓存）git rm --cached {MOD_NAME}
+ 3,提交更改到代码库，可观察到'.gitmodules'内容发生变更 git commit -am "Remove a submodule."
+ submodule适用于多语言开发，以及依赖的源代码频繁更新的状况。

## git subtree

+ git subtree 列举常用subtree命令
+ git remote add subtree_origin https://github.com/DanielTeng/git_child.git （普通的增加远程库命令）
+ git subtree add --prefix=subtree subtree_origin master (prefix=subtree是指定本地目录)(--squash,选项，是否合并子库的提交历史)
+ --squash是git merge的可选参数
+ git subtree pull --prefix=subtree subtree_origin master (subtree的pull)
+ git push, 修改subtree以后的推送，只影响主项目，跟subtree指向的子项目无关。(我猜这时对subtree做pull会导致merge并可能冲突)
+ git subtree push --prefix=subtree subtree_origin master (这是对subtree指向的子项目远程库做push，权限问题)
+ git log subtree_origin/master; 这会只看到子库的提交历史
+ --squash,要么从开始就一直用，要么就一直都不用。不然会乱。
+ parent下拉，修改，上推，child下拉，修改，上推，都没问题。这时parent下拉，报告冲突，是为什么？下回分解。

## git cherry-pick

+ branch的嫁接技术
+ git cherry-pick commit_id; 把其他分支的提交应用到本分支。
+ 因为提交都记录了代码。从分歧点，依序嫁接过来，不会有任何问题。跳岛嫁接，会产生冲突，需手工解决冲突。
+ 建议依次嫁接。

## 问：master如何撤回到上一个版本？

+ git reset --hard commit_id

## git rebase

+ git rebase, 跟merge 不同
+ git checkout feature2， git rebase feature1; feature2 就该改换成以 feature1为base的直线继续分支，两个分支也是合并了。
+ rebase把feature2的更新应用到了feature1分支上。
+ git rebase跟merge一样也可能有冲突。解决冲突后，需要git add 添加，然后执行 git rebase --continue.
+ git rebase --abort, 那就取消rebase了，分支会恢复到执行rebase之前的状态。
+ git rebase 会修改 feature2的提交历史，改为以feature1为base。
+ 最佳实践：不要对master做rebase；只在本地分支做rebase，尚未推送到远程，不对远程分支做rebase。
