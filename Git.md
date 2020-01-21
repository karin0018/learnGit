# Git

##本地仓库

git commit 提交记录

git branch … 创建新的分支

git checkout -b <your- branch-name> 创建新的分支同时切换过去

git merge <branch name > 合并分支

git checkout … 切换分支/master

**Git Rebase** 合并分支的另一种方法，实际上就是取出一系列的提交记录，复制他们，然后在另外一个地方逐个放下去；

rebase 的优势是可以创造更线性的提交历史，能是代码库的提交历史变得异常清晰。

git rebase master;//接到master的后面

git rebase <branch>;//接到branch的后面

git master~<num> ;//head 向上回溯num个位置，指向master的第num个父亲记录；

**移动分支**：将某个分支强制移动到某个指定节点；

git branch -f master HEAD~3 ;//-f  将master的分支强制指向 HEAD 的第三级父提交；

**撤销变更**：git reset ; git revert;

git reset HEAD~1 ;//向上移动分支，原来指向的提交记录被丢到暂存区，不在本地代码库中；

git revert HEAD;//本地使用的reset对远程分支无效，revert 可以将更改分享给别人；

**整理提交记录**：git cherry-pick <提交号>；（需要已知提交记录的hash值）

可以将提交树上任何地方的提交记录，复制到当前所在位置**HEAD**下面；

**交互式rebase**：使用带参数 interactive 的rebase命令，简写为 -i

git rebase -i HEAD~4;

**本地栈式提交**

git rebase -i 将提交重新排序，把我们想要修改的提交记录挪到最前；

commit –amend 进行一些修改

git rebase -i 将记录调整为原来的顺序；

最后把master移动到在修改的最前端

**Git Tags** 

git tag v1 c1 //将一个标签命名为v1，负责指向提交记录c1如果不指定提交记录，该标签会指向HEAD指向的位置；

**Git Describe**

描述离自己最近的tag；

git bisect //用于查找产生Bug的提交记录的指令。

git describe <ref> //ref 可以是任何能被Git识别成提交记录的引用，如果没有指定，默认为 HEAD；

##远程仓库

配置环境 git clone //在本地创建一个远程仓库的拷贝 

**远程分支 - 在本地仓库中的**<remote name>/<branch name>

反映了远程仓库在自己上一次访问时的状态，用于理解本地工作与公共工作的差别；

远程仓库一般被命名为 origin

**Git Fetch**:从远程仓库获取数据，是本地与远程仓库的通信方式

- 从远程仓库下载本地仓库中确实的提交记录；

- 更新远程分支指针；origin/master

    实际上将本地仓库中的远程分支更新成了远程仓库中相应分支最新的状态；

- git fetch 不会改变本地仓库的状态，不会更新master分支，不会修改磁盘上的文件。

- 可以理解为单纯的下载操作

**Git Pull**：先抓取更新，再合并到本地

git pull ==  git fetch + git merge 

**Git Push**：将本地的变更上传到指定的远程仓库，并在远程仓库上合并自己的新的提交记录；

git push 完成之后，同一team的人即可下载你的更新；

**Git pull –rebase** ：基于远程仓库更新快于本地；

**远程追踪分支** 

git checkout -b foo origin/master ；

或者

git branch -u o/master foo

如果省略 foo 则 默认值为当前分支

可以创建一个名为 foo 的分支，他追踪远程分支 origin/master ，替代原先的 master

**Git Push 的参数**

git push <remote> <place>

```
git push origin master
```

把这个命令翻译过来就是：

*切到本地仓库中的“master”分支，获取所有的提交，再到远程仓库“origin”中找到“master”分支，将远程仓库中没有的提交记录都添加上去，搞定之后告诉我。*

## 创建版本库

mkdir + 文件名；新建一个文件夹

cd + 文件名；打开一个文件夹

pwd 显示当前目录

git init 创建git仓库

添加文件到git仓库：

git add file;//添加文件到暂存区；

 git commit -m "message”;

时刻掌握仓库当前状态： git status 

查看上次修改的内容 ：git diff;//difference

查看提交日志 ：git log;

查看提交结点的hash值： git log –pretty=oneline;

查看文件内容 ： cat file_name;

git reflog //记录了每一次命令；

**HEAD**指向当前版本； git reset –hard commit_id //允许我们在各个版本之间穿梭；

## 远程仓库

关联远程仓库：git remote add origin git@server-name:path/repo-name.git

第一次提交本地仓库的内容: git push -u origin master

git push origin master;//向远程仓库 origin 推送本地分支master；



