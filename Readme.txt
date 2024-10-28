1、配置： 
    - name 
        git config --global user.name "wangguixiang"
    - email
        git config --global user.email "995197535wang@gmail.com"

2、使用git：
    - git status    
        查看当前仓库的状态
    - git init      
        初始化仓库
    - git log       
        查看修改log

    有没有被git管理，就看有没有.git文件夹

3、状态：
    未跟踪（U）
    已跟踪：
        暂存    已保存，没有提交git仓库
        提交    和git仓库相同
        已修改（M）  修改，和git仓库不同

    刚刚添加到项目中的文件，属于未跟踪状态
        - 未跟踪 --> 暂存（绿色）
            git add <filename>      
                将文件切换到暂存状态
            git add *               
                将所有已修改（未跟踪）的文件暂存
        - 暂存 --> 提交
            git commit -m""         
                将暂存的文件存储到仓库中
            git commit -a -m""      
                提交所有已修改的文件（未跟着的文件不会提交）
        - 未修改 --> 修改（红色   modified）
            修改代码后，文件会变为修改状态

4、常用的命令
    - git restore <filename>  
        重置文件
    - git restore --staged <filename>  
        暂存的状态取消

    - git rm <filename>  
        删除文件
    - git rm <filename> -f  
        强制删除文件

    - git mv <filename1> <filename2>  
        移动文件 重命名文件

        注意：git rm <filename>后没有完全删除，进入暂存模式
            - git commit -m"xxx" 后完全删除（提交）
            - git restore --stage <filename> 取消暂存模式
                git restore <filename> 可以恢复

5、分支
    git在存储文件时，每一次代码的提交都会创建一个对应的节点，git就是通过一个一个的节点，记录代码的状态

    默认情况下仓库只有一个分支，命名为master。

    分支与分支之间相互独立，互不影响

    操作
        - git log  
            查看log，按q取消
        - git branch  
            查看分支
        - git branch <branch name> 
            创建分支
        - git branch -d <branch name> 
            删除分支
        - git switch <branch name> 
            切换分支
        - git switch -c <branch name> 
            切换到新创建的分支

    开发第一件事，创建分支
    开发中，在自己的分支写代码，将自己的分支，合并到主分支中

    合并
        - git merge <branch name>  
            合并
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

    - git branch -M main  
        修改分支的名字

    - git push  
        将代码上传到服务器上

    将本地库上传github

        git remote add origin https://github.com/Harry97535/git-demo.git
        git branch -M main
        git push -u origin main

8、远程库操作命令
        - git remote  
            显示当前关联到的所有远程库
        - git remote add <远程库名字> <url>  
            关联远程库
        - git remote remove <远程库名字>  
            删除远程库

        - git push -u <远程库名字> <分支名>  
            向远程库推送代码，和当前分支关联
        - git push  
            直接推送
        - git push <远程库> <本地分支>:<远程分支>
            将本地分支推送到远程库的远程分支

        - git clone <url>  
            从远程库下载代码

    注意：如果本地库的版本低于远程库，push推不上去
    必须确保本地库和远程库的版本一致
        - git fetch
            - fetch从远程库下载所有代码，但是，不会将代码和当前分支自动合并
            - 使用fetch后，必须合并   git merge origin/main

        - git pull 也是拉取
            - 从服务器拉取代码，并自动合并
    推送代码之前，一定要先从远程库中拉取最新的代码 

9、tag标签
        当头指针没有执行某个分支的头部时，这种状态称为分离头指针，在这种状态下，也可以修改代码
    这些操作，不会出现在任何的分支上，不要再分离头指针状态下操作代码
        如果非要后面的节点操作，先创建分支再操作
        头指针：现在代码的位置
        - git switch 节点
        - git switch -c <分支名> <提交id>

        tag为提交记录设置标签
        - git tag   
            查看标签
        - git tag <标签名>   
            添加标签
        - git tag <标签名> <提交id>   
            给某个id添加标签
        - git push <远程仓库> <标签名>   
            上传这个标签到远程库中
        - git push <远程仓库> --tags
            全部上传到远程库
        - git tag -d <标签名>   
            删除标签（本地的）
        - git push <远程仓库> --delete <标签名>   
            删除远程标签

10、gitignore
    默认情况下，git会监视项目中所有内容，但是有一些内容，比如node_moduler，不希望它被git管理
    我们可以在项目目录中，添加gitignore文件，来设置那些需要git忽略的文件

    - 添加gitignore文件   

11、github静态页面
    - git中，可以将自己的静态页面部署到github，会提供一个地址，变成真正的网站
        要求：
            - 静态页面的分支必须叫：gh-pages
                git branch -M gh-pages
            - 如果希望通过 xxx.github.io 访问
                需要将库的名字配置为 xxx.github.io

12、docusaurus简介

    - facebook推出的开源的、静态的内容管理系统，可以快速的部署一个人静态网站
    - 使用
        - 安装
        