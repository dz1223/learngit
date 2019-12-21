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


- 
