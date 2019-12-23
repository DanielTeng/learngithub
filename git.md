## 获得版本库
+ git init
+ git clone

<br>

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

<br>

## 查看信息
+ git help
+ git log
+ git log -5 （只查最近5条提交信息）
+ git log --pretty=oneline
+ git log --pretty=format:"%h -%an, %ar :%s"
+ git dif
+ git status (当前git状态)

<br>

## 远程协作
+ git push
+ git pull

<br>

## 配置操作
+ git config (git config --global user.name "Your Name")
+ git config (git config --global user.email "Your Email")
+ git config --global --replace-all user.name "Daniel_Teng"
+ git config --global --replace-all user.email "tengyong1971@gmail.com"
+ git config --list
+ system -> global -> local 系统 -> 用户 -> 项目
+ git help config
+ git config --help
+ man git-config (这需要linux系统)

## 撤销工作区操作
+ git checkout -- test.txt

## 文件重命名
+ git mv test.txt test1.txt (move)
