1、配置： 
    - name 
        git config --global user.name "wangguixiang"
    - email
        git config --global user.email "995197535wang@gmail.com"

2、使用git：
    - git status    查看当前仓库的状态
    - git init      初始化仓库
    - git log       查看修改log

    有没有被git管理，就看有没有.git文件夹

3、状态：
    未跟踪（U）
    已跟踪：
        暂存    已保存，没有提交git仓库
        提交    和git仓库相同
        已修改（M）  修改，和git仓库不同

    刚刚添加到项目中的文件，属于未跟踪状态
        - 未跟踪 --> 暂存（绿色）
            git add <filename>      将文件切换到暂存状态
            git add *               将所有已修改（未跟踪）的文件暂存
        - 暂存 --> 提交
            git commit -m""         将暂存的文件存储到仓库中
            git commit -a -m""      提交所有已修改的文件（未跟着的文件不会提交）
        - 未修改 --> 修改（红色   modified）
            修改代码后，文件会变为修改状态

4、常用的命令
   - git restore <filename>  重置文件
   - git restore --staged <filename>  暂存的状态取消

   - git rm <filename>  删除文件
   - git rm <filename> -f  强制删除文件

   - git mv <filename1> <filename2>  移动文件 重命名文件

    注意：git rm <filename>后没有完全删除，进入暂存模式
        - git commit -m"xxx" 后完全删除（提交）
        - git restore --stage <filename> 取消暂存模式
            git restore <filename> 可以恢复

5、分支
    git在存储文件时，每一次代码的提交都会创建一个对应的节点，git就是通过一个一个的节点，记录代码的状态

    默认情况下仓库只有一个分支，命名为master。

    分支与分支之间相互独立，互不影响

    操作
        - git log  查看log，按q取消
        - git branch  查看分支
        - git branch <branch name> 创建分支
        - git branch -d <branch name> 删除分支
        - git switch <branch name> 切换分支
        - git switch -c <branch name> 切换到新创建的分支

    开发第一件事，创建分支
    开发中，在自己的分支写代码，将自己的分支，合并到主分支中

    合并
        - git merge <branch name>  合并
        - 记录非常细，项目复杂，分支太多，代码记录混乱
        
6、变基（rebase），也可以合并
        1. 变基时，git找到两条分支的最近的焦点（共同祖先）
        2. 对比当前分支相对于祖先的历史提交（找不同），将不同提取出来，存储到临时文件中
        3. 将当前部分指向目标的基底
        4. 以当前基底开始，重新执行历史操作
   
    例：
        - 在bug中
            变基：git rebase master(main)
            回master：git switch master
            合并：git merge bug

    变基和merge合并分支，结果是一样的
        - 变基的提交记录更整洁，更清晰
        - 大部分情况，合并和变基可以互换的
        - 但是！！！ 如果分支已经提交给远程仓库，尽量不要使用变基

        -本地变基完成后，再传服务器上


7、远程仓库（remote）
    - 实际开发中，git的服务器通常由公司搭建内部使用或者购买一下公共的私有git服务器
    - 学习阶段，可以使用开放的git仓库，常用：GitHub和Gittee（码云）

                     远程库的名字   远程库的地址
    - git remote add <remote name> <url>

    - git branch -M main  修改分支的名字

    - git push  将代码上传到服务器上

    将本地库上传git

        git remote add origin https://github.com/Harry97535/git-demo.git
        git branch -M main
        git push -u origin main


        