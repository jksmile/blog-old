
## Git常用操作

*   [基础操作](#basicAction)

*   [快捷命令设置](#fastAction)

*   [彩色交互界面](#colorUI)

*   [设置个人信息](#setInfo)

*   [设置远程仓库](#setRemote)


***


<h3 id="basicAction">基础操作<h3>

    # 提交修改
    git add /path/to/file
    git commit -m 'reason'

    # 提交全部修改
    git commit -a -m reason

    # 创建本地分枝
    git co -b branch_name

    # 查看本地分枝
    git branch

    #查看远程分支
    git branch -r

    # 删除分支
    git branch -D branch_name

    # 查看分支之间的差异
    git diff master branch

    # 查看最新版本和上一个版本的差异(一个^表示向前推进一个版本)
    git diff HEAD HEAD^

    # 查看状态
    git status

    # 合并目标要支到当前分支
    git merge targetBranch

    # 销毁自己的修改
    git reset --hard


<h3 id="fastAction">快捷命令设置</h3>

    git config --global alias.st status

    git config --global alias.ci "commit -a"

    git config --global alias.co checkout

    git config --global alias.br branch

    git config --global alias.dc dcommit

    git config --global alias.rb rebase


<h3 id="colorUI">彩色交互界面</h3>

    git config --global color.branch auto

    git config --global color.diff auto

    git config --global color.interactive auto

    git config --global color.status auto

    git config --global core.autocrlf input


<h3 id="setInfo">设置个人信息</h3>

    git config --global user.name "your_name"

    git config --global user.email "your_name@mail.com"



<h3 id="setRemote">设置远程仓库</h3>

#### 本地非GIT项目，PUSH到远程仓库
    #初始化git
    git init

    #添加文件至git管理  【git add . 表示当前目录下所有文件】
    git add /path/to/file

    #提交添加的文件
    git commit -m "first commit"

    #添加远程地址
    git remote add origin https://github.com/test.git

    #push到远程仓库
    git push -u origin master


#### 本地GIT项目，PUSH到某远程仓库
    #改变GIT远程仓库地址
    git remote add origin https://github.com/test.git

    #push到远程仓库
    git push -u origin master

    #本地GIT新分支，推到远程仓库
    git --set-upstream





