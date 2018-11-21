# git 学习
## 创建本地仓库，提交文件到从工作区到暂存区，并指向一个HEAD
>下载安装本地gitbase
```
    - mkdir test_repository
    - cd test_repository
    - git init
    - git add filename
    - git commit -m "说明"
```
## git 三个状态切换[工作区、暂存区、本地仓库]

    git add filename  从工作区添加到暂存区

    git commit -m "说明"

    gti chechout filename  丢弃工作区改变

    git reset  filename   从暂存区退到工作区

    git reset  --hard  commit_id  版本回退，丢弃修改内容

    git reset  --soft  commit_id  版本回退，将内容放入暂存区
## 版本回退
```
    - git status 查看所有的修改状态
    - git diff filename  查看文件修改的地方
    - git log 查看git的提交历史，可以查看到head号, 可以回退到过去
    - git reflog 查看命令历史，可以查看到commit号，可以回到未来
    - git reset --hard HEAD^  回退到上一版本，HEAD^^ 上上版本， 可以一直^^^,HEAD指向的版本就是当前版本
    - 通过git reset --hard commit_id 结合log可以进行版本之间的切换
```
## 管理修改
```
git diff HEAD --filename   查看工作区和暂存区的不同
```
## 本地仓库撤销修改
> 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时
```
用命令git checkout -- file。
```
> 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步
```
第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
```
> 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，进行版本回退
```
git reset --hard commit_id ，不过前提是没有推送到远程库。
```
## 本地仓库删除文件/撤销删除
> 场景1：该文件在删除之前已commit到暂存区中了，手动或rm后，确定要从版本库中删除该文件，
```
那就用命令git rm filename删掉，并且git commit -m "xxx"
```
> 场景2：该文件在删除之前已commit到暂存区中了，误删了，想恢复，
```
那就执行git checkout -- filename 恢复到最新版本，【缺点是此版本后的修改都丢失了】
```
> 场景3：该文件在删除之前只add到暂存区了，误删了，
```
git checkout -- filename 就可恢复之前add后版本的状态，然后git commit 就可以将之前add的状态保存，add后的丢失
```
注：
- 只要放到了暂存区无论是add还是commit或git rm了，都可以通过checkout恢复，唯一缺点是上次提交后的修改会丢失；
- git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”;



## 分支管理
- 查看分支
```
git branch
```
- 创建分支
```
git branch  <name>
```
- 删除分支
```
git branch -d <name>
```
- 切换分支
```
git checkout <name>
```
- 合并分支
```
git merge <name>

将name分支合并到当前分支，将子合到主
-- 冲突只能手动解决
-- 解决完冲突记得提交
```
## 标签管理
- 查看标签
```
git tag
```
- 创建标签
```
git tag <name><commit_id> 给指定的版本加标签
```
- 删除标签
```
git tag -d <name>
```





## 一、git上传异常解决

使用Git上传本地文件到github时，一直报错，终于被解决。

    git add .

    git commit -m"peTzxz"

    git push origin master

当执行到push时，就会报错，报错代码如下：

MacBook-Pro:数据库课程设计 Pett$ git push origin master
>To github.com:peTzxz/Property-management-system
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:peTzxz/Property-management-system'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

出现这个问题是因为github中的README.md文件不在本地代码目录中，可以通过如下命令进行代码合并
```
git pull --rebase origin master
```
然后再
```
git push origin master
```
便可上传成功

[markdown基础语法学习链接](https://github.com/younghz/Markdown "Markdown")
***

## 本地已经存在的项目如何和github发生关联
1. github新建repository
2. 解除原有仓库关联
3. 本地仓库与远程仓库解除关联 rm -rf .git 删除该仓库的工作树即可 第2、3步可以在第4步之后执行
切换到本地项目地址 git init 初始化项目。该步骤会创建一个 .git文件夹是附属于该仓库的工作树。
```
git init
git add .
git commit -m 'initial commit'
git remote add origin git@github.com:xx/aaaaa.git
```
这时候push一般会说reject，因为创建仓库的时候新建了readme文件，与原仓库文件发生了冲突。

一个方法是创建的时候不要勾选创建readme，另一个方法是：
```
git pull origin master
git commit -a
```
pull可能会出现冲突，自动合并也会出错，这时候要打开readme文件，里面会多了“<<<”“>>>>123”这样的符号， 就自行选择需要的，把这两行删除了。
最后再：
```
push -u origin master
```
把本地项目push到远程github仓库
