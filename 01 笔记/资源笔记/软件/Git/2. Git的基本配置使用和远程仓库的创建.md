---
onenote-id: 0-69086c3370434465a89eadb2cf8f973e!1-DBD29CD2C5C95FE5!sea6e119cfc944e4786d831c26c2cda79
---
**Git****基本指令**

|   |   |
|---|---|
|ls/ll|查看当前文档|
|cat|查看文件内容|
|touch|创建文件|
|vi|vi编辑器（使用vi编辑器是为了方便展示效果，学员可以记事本、editPlus、notPad++等其他编辑器）|
 
**基本配置**  
设置用户信息

|   |   |
|---|---|
|1  <br>2|git config **--**global user**.**name "用户名"  <br>git config **--**global user**.**email "邮箱地址"|

查看配置信息

|   |   |
|---|---|
|1  <br>2|git config **--**global user**.**name  <br>git config **--**global user**.**email|

**常用指令配置别名**  
打开用户目录，创建.bashrc文件

|   |   |
|---|---|
|1|touch ~**/.**bashrc|

在.bashrc文件中输入如下内容

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//用于输出git提交日志  <br>alias git**-**log**=**'git log --pretty=oneline --all --group --abbrev-commit'  <br>//用于输出当前目录所有文件及基础信息  <br>alias ll**=**'ls-al'|

打开gitBash，执行source ~/.bashrc

|   |   |
|---|---|
|1|source ~**/.**bashrc|

**解决****GitBash****乱码问题**  
打开GitBash执行下面命令

|   |   |
|---|---|
|1|git config **--**global core**.**quotepath **false**|

${git_home}/etc/bash.bashrc 文件最后加入下面两行

|   |   |
|---|---|
|1  <br>2|export LANG**=**'zh_CN.UTF-8'  <br>export LC_ALL**=**'zh_CN.UTF-8'|

**获取本地仓库**

1. 在电脑的任意位置创建一个空白目录（例如test）作为我们的本地Git仓库
2. 进入这个目录中，点击右键打开Git bash窗口
3. 执行命令git init
4. 如果创建成功后可在文件夹下面看到隐藏的.git目录

|   |   |
|---|---|
|1  <br>2|git init //初始化当前目录为一个git仓库  <br>//初始化文件后当前目录下会出现多一个.git文件夹|

**基础操作指令**

|   |   |   |
|---|---|---|
|仓库（repository）|暂存区（index）|工作区（workspace）|
|修改进入到仓库就变成了一次提交记录|提交到仓库之前的缓存区（已暂停  <br>存）staged|1. 修改已有文件（未暂存）unstaged<br>2. 新创建一个文件（未跟踪）untracked|

|   |   |
|---|---|
|1|git status //查看的修改的状态（暂存区、工作区）|

查看修改的状态status

添加工作区到暂存区add

|   |   |
|---|---|
|1  <br>2|git add 单个文件名**\|**通用符 //添加工作区一个或多个文件的修改到暂存区  <br>git add **.** //将所有修改加入暂存区|

提交暂存区到本地仓库commit

|   |   |
|---|---|
|1|git commit **-**m '注释内容' //提交暂存区内容到本地仓库的当前分支|

查看提交日志log

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|git log **--**all //显示所有分支  <br>git log **--**pretty**=**oneline //将提交信息显示为一行  <br>git log **--**abbrev**-**commit //使用输出的commitid更简短  <br>git log **--**graph //以图的形式显示|

版本回退

|   |   |
|---|---|
|1|git reset **--**hard commitID //版本回退，commitID可以使用git log 或git-log指令查看|

查看已经删除的记录

|   |   |
|---|---|
|1|git reflog //查看已经删除的指令|

添加不需要进行管理的文件，创建.gitignore文件，编辑内容*.a，表示后缀为a的文件不会被添加

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|touch **.**gitignore  <br>vi **.**gitignore  <br>//输入文本  <br>***.**a|

删除文件

|   |   |
|---|---|
|1|rm 文件名|

修改文件名

|   |   |
|---|---|
|1|mv 原文件名 修改文件名|

**git****分支常用指令**

查看本地分支

|   |   |
|---|---|
|1|git branch|

创建本地分支

|   |   |
|---|---|
|1|git branch 分支名|

切换分支checkout

|   |   |
|---|---|
|1|git checkout 分支名|

切换一个不存在的分支，git会创建并切换

|   |   |
|---|---|
|1|git checkout **-**b 分支名|

合并分支merge

|   |   |
|---|---|
|1|git merge 分支名称|

删除分支  
不删除当前分支，只能删除其他分支

|   |   |
|---|---|
|1  <br>2|git branch **-**d b1 //删除分支时，需要做各种检查  <br>git branch **-**D b1 //不做任何检查，强制删除|

**开发中分支使用原则与流程**

- master（生产）分支

线上分支，主分支，中小规模项目作为运行的应用对应的分支。

- develop（开发）分支

是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要时合并到master分支，准备上线。

- feature/xxx分支

从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到develop分支。

- hotfix/xxx分支

从master派生的分支，一般作为线上bug修复使用，修复完成后需要合并到master，test，develop分支。

**远程仓库操作**

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|git remote add origin git@xxxxx**.**git远程仓库地址 //连接远程仓库  <br>git remote //查看仓库  <br>git push **[-**f**] [--**set**-**upstream**] [**远端名称 **[**本地分支名**]:[**远端分支名**]]**  <br>git push origin master**:**master //推送到远端仓库|

注意：其中--set-upstream指推送到远端的同时并且建立起和远端分支的关联关系。  
-f为强制将本地仓库覆盖远程仓库。

查看本地分支和远程分支之间的关系

|   |   |
|---|---|
|1|git branch **-**vv|

**从远程仓库克隆**  
如果已经有一个，我们可以直接clone到本地。

- 命令：git clone \<仓库路径\> [本地路径]
	- 本地目录可以省略，会自动生成一个目录。

|   |   |
|---|---|
|1|git clone git@gitee**.**com**:**zhu_jiao**/**git_test**.**git|

**从远程仓库中抓取和拉取**  
远程分支和本地的分支一样，我们可以进行merge操作，只是需要先把远程仓库里的更新都下载到本地，再进行操作。

- 抓取命令：

|   |   |
|---|---|
|1|git fetch **[**remote name**] [**branch name**]**|

- **抓取命令就是将仓库里的更新都抓取到本地，不会进行合并。**
- 如果不指定远端名称和分支名，则抓取所有分支。

- 拉取命令：

|   |   |
|---|---|
|1|git pull **[**remote name**] [**branch name**]**|

- **拉取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于****fetch + merge****。**
- 如果不指定远端名称和分支名，则抓取所以并更新当前分支。

**解决合并冲突**  
在一段时间，A和B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突。  
A用户在本地修改代码后优先推送到远程仓库，此时B用户在本地修改代码，提交到本地仓库后，也需要推送到远程仓库，此时B用户晚于A用户，**故需要先拉取远程仓库的提交，经过合并后才能推送到远端分支。**  
在B用户拉取代码时，因为A、B用户同一段时间修改了同一份文件的相同位置代码，故会发生合并冲突。  
**远程分支也是分支，所以合并时冲突的解决方式和解决本地分支冲突相同**。