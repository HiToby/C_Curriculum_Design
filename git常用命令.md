## 以下几个是git常用的指令，可以简单了解一下。

### 1）git config

在使用git前最好先配置一下你的个人信息及使用偏好。以下命令的意思就不用解释了吧，执行完以下命令就会在你的家目录（~）下生成一个文件~/.gitconfig。
```git
$ git config --global user.name "username"  
$ git config --global user.email test@163.com  
$ git config --global core.editor vim  
$ git config --global merge.tool vimdiff  
$ git config --global color.status auto  
$ git config --global color.branch auto  
$ git config --global color.interactive auto  
$ git config --global color.diff auto  
$ git config --global push.default simple  
$ git config --global alias.co checkout  
$ git config --global alias.ci commit  
$ git config --global alias.st status  
$ git config --global alias.last 'log -1 HEAD'  
$ git config --global alias.unstage 'reset HEAD --'  
```
### 2）git add

添加文件内容到索引中去（暂存文件），几个简单示例：
```git
$ git add .  
$ git add --all  
$ git add *.txt  
$ git add directory/*.sh  
```
突然你又不想git add了，那么执行以下命令：
```git
$ git reset .  
$ git reset *.txt  
$ git reset directory/*.sh  
```
### 3）git rm

删除索引和当时工作目录中的文件。
```git
$ git rm filename  
$ git rm -f *.txt  
$ git rm -r .  
```
### 4）git commit

将当前改动记录到仓库中，即提交改动到本地仓库中。

	$ git commit -m "add a file and remove a file"  

突然你又不想git commit了，那么执行以下命令:

	$ git reset HEAD^  	

你commit之后发现少添加了一个文件：
```git
$ git commit -m'msg'  
$ git add forget_file  
$ git commit --amend  
```
你的 commit 已经 push 到远程分支(master)了，现在你想反悔了：
```git
$ git clone git@github.com:username/test.git  
$ cd test  
$ git reset HEAD^  
$ git push -f master   
```
### 5）git status

查看当前工作目录的状态，即修改、添加及删除了哪些文件。

	$ git status  

### 6）git checkout

检出一个分支和目录到当前工作目录中，可以简单理解为切换分支的命令。

以下命令分别为切换到分支 branch1 和创建一个新的分支 new_branch 。

	$ git checkout branch1  
	$ git checkout -b new_branch  

取消本地改动：

	$ git checkout -- file_name  

### 7）git branch

列出、创建和删除分支。

以下指令分别为列出本地分支、所有分支、远端分支、创建、删除、强制删除分支。
```git
$ git branch --list  
$ git branch --all  
$ git branch --remotes  
$ git branch new_branch  
$ git branch --delete branch_name  
$ git branch -D branch_name  
```
删除remote tracking branch，就是git branch -r命令列出的分支。
```git
$ git branch -r  
$ git branch -d -r origin/develop  
```
### 8）合并分支

如果出现冲突，那么手动解决冲突就可以了。
```git
$ git checkout branch_name  
$ git checkout master  
$ git merge branch_name  
```
### 9）删除远程分支

合并分支之后如果不再需要以前的分支了，那么可以在本地及远程删除它。
```git
$ git branch -d branch_name  
$ git branch -D branch_name  
$ git push origin :branch_name  
```
这条命令耐人寻味啊，其中origin是你的远程仓库名字（git remote -v可以查看到）。

### 10）git diff

查看改动内容。
```git
$ git diff filename  
$ git diff .  
$ git diff revision1 revision2  
$ git diff branch1 branch2  
```
DIFF暂存（添加到索引中）的文件：
```git
$ git add .  
$ git diff --cached  
```
View the redundant Tab or Space in your codes:
```git
$ git diff --check  
$ git diff --check --cached  
```