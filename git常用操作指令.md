---
date: 2018-05-17 09:21
status: public
title: git常用操作指令
---

## git study
####创建版本库
1. git init 命令用于在当前文件夹内创建新的“仓库”repository. 
2. git add <file> 命令将文件添加到版本库中， 例如  git add readme.md 
	add 成功后不会有提示，没有提示就没有错误
3. git commit -m "..." 命令提交你 add 或者 改动过的代码 例如 ： 
	git commit -m "create a readme.md file"

   `[master (root-commit) bbdcff7] create a readme.md file 
	1 file changed, 1 insertion(+)
	create mode 100644 readme.md`		
"" 内的内容是你对提交文件的描述，方便在版本控制库中查找之间的修改
	提示一个文件改变了，插入了一行（因为readme中有一行内容）

####查看修改过的内容
1. git status 命令查看当前仓库状态：那些文件被修改过
2. git diff <file> 产看当前文件和仓库中文件的不同处。

####返回到之前的版本 
1. git reset HEAD^|版本号  其中HEAD^ 是上一版本，git中将当前版本定为HEAD 而HEAD^ 是上个版本，
 HEAD^^ 是上上个版本
2. git reflog 可以产看每次的命令和所操作的 commit id. 可以根据id来进行回退或者版本更替。

####当前分支和暂存区
1. 当前分支： 在默认情况下，git在我们使用 *init* 命令创建分区时，会为我们创建唯一一个 *master* 分支，我们在使用*commit* 提交文件时就是提交到 *maste* 分支。
2. 暂存区：在 .git 文件夹下存在一个stage(或者叫index)的暂存区，我们通过*git add* 命令就是将修改或新添加的文件放入暂存区，以便之后通过commit提交到版本库（Repository）中。

####撤销修改
1. git  checkout -- file  在修改了文件，还没有add到暂存区，可以使用*checkout*命令进行撤销操作。
2. git reset HEAD <file> 修改了文件，并且已经通过add命令提交到了暂存区，可以使用reset HEAD <file>命令将暂存区中的文件撤销（unstage）,重新放回工作区。注意，工作区的文件并不会撤销，只是将暂存区的修改撤销了而已。
3. git reset 不仅可以进行版本回退（前提是没有推送到远程库），还可以撤销add进暂存区中修改。

####删除文件
通常我们删除文件时，直接选择delete掉或者使用命令行操作 rm 进行删除。但是这样只是在工作区中进行了删除，版本库中的文件并没有改变。如果只把工作区的文件删除后再使用git status 命令产看状态时：

    $ git status
        On branch master
         Changes not staged for commit:
        (use "git add/rm <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)
         deleted:    test.txt
          no changes added to commit (use "git add" and/or "git commit -a")
    

1. git rm 从版本库中删除文件并通过 commit 提交删除。

2.git checkout -- <file> 从版本库中恢复文件到工作区。