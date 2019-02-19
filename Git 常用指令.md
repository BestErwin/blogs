# Git 常用指令

版本查询

    git --version

设置当前用户信息

    // 根据个人信息替换引号内的内容
    git config --global user.name "xxx"
    git config --global user.email "xxx@xxx"

显示当前用户信息

     git config --list
    或
     git config -l

显示git常用指令

    git

初始化仓库

    // xxx 代表仓库名/文件夹名
     mkdir xxx
     cd xxx
     git init
    或
     git init xxx

远程仓库

    // xx 指远程名称， xxx指远程地址
    // 如果是git clone得到的仓库，远程名称默认为origin
    // 添加远程仓库
    git remote add xx xxx
    // 查询远程仓库名
    git remote
    // 查询远程仓库详细信息
    git remote -v
    // 复制远程仓库
    git clone
    // 提交至远程仓库
    git push -u xx xxx
    // 将本地与远程同步
    git pull 或 git fetch && git merge

查询仓库状态

    git status

将文件添加到暂存区

    git add.

生成“后悔药”

    git commit -m "xxx"

“后悔药”查询

    // 基本查询
    git log
    // 详细查询，包括修改对比
    git log -p
    // 以精简模式显示
    git log --oneline
    // 查看“后悔树”
    git log --graph

吃“后悔药”，版本回退

    // xxx 代表编号或标记，可用git log查询
    git checkout xxx
    // 回退到最近的版本
    git checkout -

标记

    git tag
    // xx 代表标记， xxx代表注释
    git tag -a xx -m "xxx"
    // 显示标记
    git show xx

分支

``` 
// xxx代表分支名
// 产生分支
git branch xxx
// 分支跳转
git checkout xxx
// 创建并跳转分支
git checkout -b xxx
// 合并分支
git merge
```