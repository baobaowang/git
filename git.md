#### 安装git 
1. ubuntu下
    ```shell
    sudo apt-get install git
    ```
2. 安装完成后需要设置git
    ```shell
    git config --global user.name "you name"
    git config --global user.email "you email"
    ```
#### 创建版本库
1. 在需要创建版本库的文件夹下执行：
    ``` shell
    git init
    ```

#### 版本回退
1. 把文件添加到暂存区
    ```shell
    git add 文件名.后缀
    git add 文件名2.后缀
    git add 文件名3.后缀
    ```
2. 把文件提交到仓库
    ```shell
    git commit -m "这次提交的说明"
    ```
3. 查看仓库状态
    ```shell
    git status
    ```
4. 查看修改内容
    ```shell
    git diff
    ```
5. 查看历史记录
    ```shell
    git log
    ```
    如果觉得输出信息太多，可以加上：--pertty=oneline
    ```shell
    git log --pretty=oneline
    ```
6. 版本回退
    ```shell
    git reset --hard HEAD^
    ```
    HEAD后面的^^表示上个版本，^^^表示上上个版本。
    也可以根据commit id（提交id）回退：
    ```shell
    git reset --hard xxxxxx
7. 查看操作的每一条记录(命令历史)
    ```shell
    git reflog
    ```
#### 工作区和暂存区
1. 工作区就是电脑上的文件，  
    当前文件夹下的.git是一个版本库，版本库分两部分，1是git add添加的暂存区，2是 git commit提交到当前分支.  
2. 管理修改    
    没有git add 的文件不会提交到当前分支
    ```shell
    查看工作区和版本库最新版本的区别：
    git diff HEAD -- 文件名.后缀
    ```
#### 撤销修改
1. 放弃工作区的修改
    ```shell
    用版本库中的版本替换工作区的版本
    git checkout -- 文件名.后缀
    ```  
2. 撤销暂存区的修改
    ```shell
    git reset HEAD 文件名.后缀
    ```
    >如果修改了内容：
    >>1. 没有添加到暂存区：git checkout -- 文件名.后缀 
    >>>2. 已经添加到暂存区：git reset HEAD 文件名.后缀，执行1.
    >>>>3. 已经提交到分支：版本回退
#### 删除文件
1. 如果想删除一个文件
    在工作区删除后，在git中也要删除
    ```shell
    git rm 文件名.后缀
    git commit -m "删除了 xxx"
2. 删错了可以用版本库中的版本替换工作区的版本
    ```shell
    git checkout -- 文件名.后缀
    ```

#### 远程仓库
##### 添加远程库
1. 如果用户目录下没有.ssh文件夹,.ssh文件夹下没有id_rsa,id_rsa.pub两个文件,需要创建SSH.key。
    id_rsa是私有密钥，不要泄漏出去
    id_rsa是公有密钥，可以放心的告诉任何人
    ```shell
    ssh-keygen -t rsa -C "youremail@example.com"
    ```
    >如果github访问速度太慢，尝试修改hosts：  
    http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo  
    教程连接：
    >>https://blog.csdn.net/qq_32448349/article/details/80769198  
    https://blog.csdn.net/qq_31474267/article/details/88068944
2. 关联远程仓库(把当前分支与远程仓库关联起来)
    在github上Create a new repository(创建一个新的仓库)。
    ```shell
    git remote add origin git@github.com:拥有者名/仓库名.git
    ```
3. 第一次推送分支到远程仓库
    ```shell
    git push -u origin master
    ```
4. 以后推送分支到远程仓库
    ```shell
    git push origin master
    ```
##### 从远程库克隆
1. 
    ```shell
    git clone git@github.com:用户名/仓库名.git
    ```

#### 分支管理
1. 查看分支  
    git会列出所有分支，当前分支前面会有分号
    ```shell
    git branch
    ```
2. 创建分支
    ``` shell
    git branch 分支名
    ```
3. 切换分支
    ```shell
    git checkout 分支名
    ```
4. 创建并切换分支
    ```shell
    git checkout -b 分支名
    ```
5. 合并某分支到当前分支
    ```
    git merge 某分支名
    ```
6. 删除分支 
    ``` 
    git branch -d 分支名
    ```

#### 解决分支冲突
1. **<u>分支有冲突时，无法快速合并，需要解决冲突后再合并分支</u>**
2. 查看分支图
    ```shell
    git log --graph
    ```
#### 分支管理策略
1. 一般情况下，主分支master仅用来发布新版本，不在上面干活，可以新建一个dev分支，在上面干活
2. 合并分支时不要用快速合并模式。  
    --no-ff表示禁用快速合并模式，用普通模式合并。  
    ```shell
    git merge --no-ff -m "分支描述" dev
    ```
    这样合并的分支有历史记录。
#### BUG分支
1. 把当前工作现场“储存”起来
    ```shell
    git stash
    ```
2. 从需要修复bug的分支上创建临时分支后修复bug，修复完成后合并分支。
3. 查看临时储存的工作现场
    ```shell
    git stash list
    ```
4. 恢复临时分支
    ```shell
    git stash pop
    ```
#### Feature分支
1. 每开发一个新的功能时，最好新建一个分支。  
2. 丢弃一个没有合并过的分支时,用大写D强制删除
    ```shell
    git branch -D  分支名
    ```

