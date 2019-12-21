# 廖雪峰git学习笔记



- [git命令思维导图](https://www.processon.com/mindmap/5df9b79ee4b0cfc88c3e63df)

- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

- 工作区和暂存区

  ![git add](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

  ![git commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)


- 撤销修改

  1. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
  2. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD `，就回到了场景1，第二步按场景1操作。
  3. 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用命令`git reset --hard commit_id`，不过前提是没有推送到远程库。
  
-  使用分支

   Git鼓励大量使用分支：

   查看分支：`git branch`

   创建分支：`git branch `

   切换分支：`git checkout `或者`git switch `

   创建+切换分支：`git checkout -b `或者`git switch -c `

   合并某分支到当前分支：`git merge `

   删除分支：`git branch -d `


- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

- 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

- 分支策略

  在实际开发中，我们应该按照几个基本原则进行分支管理：

  首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

  那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

  你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

  所以，团队合作的分支看起来就像这样：

  ![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

- Bug分支

  修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

  当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

  在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick `命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

-  Feature分支

  开发一个新feature，最好新建一个分支；

  如果要丢弃一个没有被合并过的分支，可以通过`git branch -D `强行删除。

- 多人协作

  - 查看远程库信息，使用`git remote -v`；
  - 本地新建的分支如果不推送到远程，对其他人就是不可见的；
  - 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
  - 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
  - 建立本地分支和远程分支的关联，使用`git branch --set-upstream-to=origin/branch-name branch-name `；
  - 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

- rebase


  - rebase操作可以把本地未push的分叉提交历史整理成直线；
  - rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

- 创建标签

  - 命令`git tag `用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
  - 命令`git tag -a  -m "blablabla..."`可以指定标签信息；
  - 命令`git tag`可以查看所有标签。

- 操作标签

  - 命令`git push origin `可以推送一个本地标签；
  - 命令`git push origin --tags`可以推送全部未推送过的本地标签；
  - 命令`git tag -d `可以删除一个本地标签；
  - 命令`git push origin :refs/tags/`可以删除一个远程标签。