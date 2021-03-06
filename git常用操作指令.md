---
date: 2018-05-17 09:21
status: draft
title: git常用操作指令
---

## git study
#### 创建版本库
1. git init 命令用于在当前文件夹内创建新的“仓库”repository. 
2. git add <file> 命令将文件添加到版本库中， 例如  git add readme.md 
	add 成功后不会有提示，没有提示就没有错误
3. git commit -m "..." 命令提交你 add 或者 改动过的代码 例如 ： 

```
  git commit -m "create a readme.md file"
  [master (root-commit) bbdcff7] create a readme.md file 
  1 file changed, 1 insertion(+)
  create mode 100644 readme.md  
```
   
"" 内的内容是你对提交文件的描述，方便在版本控制库中查找之间的修改
	提示一个文件改变了，插入了一行（因为readme中有一行内容）

#### 查看修改过的内容
1. git status 命令查看当前仓库状态：那些文件被修改过
2. git diff <file> 产看当前文件和仓库中文件的不同处。

#### 返回到之前的版本 
1. git reset HEAD^|版本号  其中HEAD^ 是上一版本，git中将当前版本定为HEAD 而HEAD^ 是上个版本，
 HEAD^^ 是上上个版本
2. git reflog 可以产看每次的命令和所操作的 commit id. 可以根据id来进行回退或者版本更替。

#### 当前分支和暂存区
1. 当前分支： 在默认情况下，git在我们使用 *init* 命令创建分区时，会为我们创建唯一一个 *master* 分支，我们在使用*commit* 提交文件时就是提交到 *maste* 分支。
2. 暂存区：在 .git 文件夹下存在一个stage(或者叫index)的暂存区，我们通过*git add* 命令就是将修改或新添加的文件放入暂存区，以便之后通过commit提交到版本库（Repository）中。

#### 撤销修改
1. git  checkout -- file  在修改了文件，还没有add到暂存区，可以使用*checkout*命令进行撤销操作。
2. git reset HEAD <file> 修改了文件，并且已经通过add命令提交到了暂存区，可以使用reset HEAD <file>命令将暂存区中的文件撤销（unstage）,重新放回工作区。注意，工作区的文件并不会撤销，只是将暂存区的修改撤销了而已。
3. git reset 不仅可以进行版本回退（前提是没有推送到远程库），还可以撤销add进暂存区中修改。

#### 删除文件
通常我们删除文件时，直接选择delete掉或者使用命令行操作 rm 进行删除。但是这样只是在工作区中进行了删除，版本库中的文件并没有改变。如果只把工作区的文件删除后再使用git status 命令产看状态时：
```
   $ git status
    On branch master
    Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    test.txt
          
    no changes added to commit (use "git add" and/or "git commit -a")
```
    

1. git rm 从版本库中删除文件并通过 commit 提交删除。

2. git checkout -- <file> 从版本库中恢复文件到工作区。

#### 建立远程仓库
1. 使用Git Bash工具生成 SSH key

> $ ssh-keygen -t rsa -C "youremail@example.com"

会在C盘用户目录下生成.ssh文件夹，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
2. 在github上创建账户，并将SSH key添加进“Account settings”，“SSH Keys”
点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容
SSH key 的作用; 识别内容是否是你本人提交。只有通过公钥和私钥验证后你才能将和远程仓库建立联系。
3. 当本地仓库中已经存在有远程仓库时，使用git remote rm origin 删除远程仓库

#### 本地已有仓库上传到远程仓库
1. 在github上创建新的仓库Repository，仓库名要和本地仓库名相同，获取到SSH方式的git连接，例如：git@github.com:s549520798/Notes.git
2. 在本地仓库目录下使用命令行：git remote add origin git@github.com:s549520798/Notes.git 将远程仓库和本地仓库合并。

> origin 是远程仓库的默认名。

3. 如果远程仓库中存在本地不存的文件时，在push之前要进行pull（pull=fetch+merge）操作，将远程文件下载到本地 ： git pull  origin master。
> 出现fatal: refusing to merge unrelated histories 错误的解决方法，使用git pull origin master --allow-unrelated-histories 命令。

4. git push origin master 将本地仓库提交到远程仓库
 
> 当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

#### 将远程仓库克隆到本地
上面的情况是先有本地库，再上传到远程仓库中；接下来的情况是，直接从远程仓库中克隆一个之前不存在的仓库到本地。
1. 在github上新建一个带readme文件的repository ，或者原先已存在的repository ，找到SSH克隆地址，如图
![](/_image/git常用操作指令/15-27-13.jpg)
2. 使用$ git clone git@github.com:s549520798/Notes.git 命令进行克隆，最好新建与repository相同的目录，在改目录下使用 git clone 命令


### 分支管理
1. 分支操作命令
git branch  产看分支
git branch <name> 创建分支
git checkout <name> 切换分支
git checkout -b <name> 创建并切换分支
git merge <name> 合并name到当前分支
git branch -d <name>删除分支
2. 使用分支进行操作基本流程

> 1. git checkout -b <name> 创建并切换到新的分支，修改文件通过 git add , commit
  到新的分支中。
> 2. git checkout master 切换到原来的分支，git merge <name>将master和新分支合并.
> 3. git branch -d <name>将新分支删除。

3. 使用分支进行操作的好处。
方便多用户创建多分支协同操作，更加安全。
    




