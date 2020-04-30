### 1、git 查看用户配置信息：git config  --list --x
global：对当前用户所有仓库有效
local：只对某个仓库有效
system：对系统所有登录的用户有效

### 2、对文件进行重命名：git mv 旧文件名 新文件
git status 查看到重命名后暂存区的提示信息为 rename
会对 暂存区 和 工作区 进行重命名不需要再次 git add

### 3、查看版本历史： git log --xx/-x
--oneline：简约查看
-n2：查看最近两次历史
--all：展示所有分支的历史，默认展示的是本分支
--graph 可以展示版本演变图
以上可以组合使用

### 4、打开git图形化界面：gitk --all(表示展示所有分支关系可选)
---

### 5、git里面的三个对象：commit tree(文件数) blob(文件)
---

### 6、切换分支：git checkout -b 分支名xxx 基于哪个分支xxx
---
例如 基于 master 创建 temp : git checkout -b temp master
基于某个分支（或者某次提交）创建分支，新创建的分支内容就会保留该基分支的内容（在暂存区）。
git log -n1 可以看到 最新的提交信息里面 (HEAD -> temp, master)
每一次提交，当前分支会前进一次，例如在temp提交一次后再次打印git log
git log -n2： (HEAD -> temp) 和 (master)两条提交信息，master不前进


### 7、比对两次提交的改变（默认跟暂存区对比）：git diff xxx xxx 
xxx可以根据 git log 打印出来的hash信息，
也可以根据HEAD HEAD^1（上一级）HEAD^1^1（上两级）
git diff HEAD^1（之前的） HEAD（目前的）

### 8、删除分支操作：git branch -d xxx(分支名)
有时候git会提示该分支没有merge的操作，确认删除此分支使用 -D

### 9、修改最近一次commit 的 message 信息：git commit --amend
编辑第一行的message，esc退出编辑，:wq保存并退出

### 10、修改以前的commit （的 message） 信息： git rebase -i 要改的父亲的hash
编辑第一行的 pick 为r（reword表示只改message），esc退出编辑，:wq保存并退出
再次编辑 message，esc退出编辑，:wq保存并退出（:q!放弃修改并退出）

### 11、合并几次commit：git rebase -i 要合并的最前的commit的父的hash
编辑要合并的 commit 的前面为s

```
 pick ddcb7ba save readme
 s 49c58fc save readme 2
 s 15eb7b7 change readme 3
 pick acfb6cc change message
```

第一行是为pick不变
最后一行是最新也不变
然后保存退出来到message继续编辑信息保存退出

### 注意 修改 commit(变基操作) 的操作比较适合在本地的自己的分支上面操作，
### 涉及他人或者远程分支的修改操作要谨慎

### 12、暂存区内容(已经git add)与当前HEAD作比较：git diff --cache
git diff 默认比较工作区与暂存区

### 13、工作区与暂存区作比较：git diff （-- 文件名）
---

### 14、（撤销add的操作）从暂存区恢复到工作区：git reset HEAD
（恢复到HEAD,HEAD如果没有其他操作，正常是指向最新的commit，可通过git log查看）
可以通过git status查看是否恢复为未 add 的状态
再通过 git diff --cached 查看暂存区与工作区无区别

### 15、想从暂存区恢复文件到工作区：git checkout -- (文件名)
注意，本地工作区的代码会被恢复
未进行 add 的代码会被 add 的代码覆盖掉

### 16、撤销commit操作回到某个commit：git reset --hard xxx(hash值)
注意工作区的东西也会回到那个commit， 谨慎操作

### 17、删除工作区文件：git rm -- (文件名)
git rm 相当于先在工作区删除文件然后git add

### 18、不使用add但是要暂存工作区内容的办法：git stash
适用场景：开发到一半接了新任务，要改动同样的东西
修改东西后未 add，先 git stash 暂存，然后进行其他开发，结束之后
git stash list 查看暂存的东西，再通过git stash pop/apply(保留list的信息)恢复工作区的内容

### 19、多人协作开发同一条远程分支
远程仓库基于master 新建 feature/add_git_commands
本地（另一个人B）克隆仓库并基于 origin/feature/add_git_commands 新建本地feature/add_git_commands
B 通过 git --config --add --local user.name/user.emal xxx设置名字和邮箱（模拟另一个）
B 在分支开发完提交 到远程分支上 origin/feature/add_git_commands

A git fetch xxx（分支名）拉取远程分支并基于远程分支新建本地分支做开发

B 开发有了新push

A开发完要push发现失败
A git fetch xxx(分支名)拉取最新到本地
A git merge origin/xxx(分支名) 合并本地和远程的新东西（B的）
A git push
git fetch + git merge = git push
