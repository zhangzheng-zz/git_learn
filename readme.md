### 1、git 查看用户配置信息：git config  --list --xx
#### global：对当前用户所有仓库有效
#### local：只对某个仓库有效
#### system：对系统所有登录的用户有效

### 2、对文件进行重命名：git mv 旧文件名 新文件名
#### git status 查看到重命名后暂存区的提示信息为 rename
#### 会对 暂存区 和 工作区 进行重命名不需要再次 git add

### 3、查看版本历史： git log --xx/-xx
#### --oneline：简约查看
#### -n2：查看最近两次历史
#### --all：展示所有分支的历史，默认展示的是本分支
#### --graph 可以展示版本演变图
#### 以上可以组合使用

### 4、打开git图形化界面：gitk --all(表示展示所有分支关系可选)

### 5、git里面的三个对象：commit tree(文件数) blob(文件)

### 6、切换分支：git checkout -b 分支名xxx 基于哪个分支xxx
#### 例如 基于 master 创建 temp : git checkout -b temp master
#### 基于某个分支（某次提交）创建分支，新创建的分支内容就会保留该基分支的内容（在暂存区）。
#### git log -n1 可以看到 最新的提交信息里面 (HEAD -> temp, master)
#### 每一次提交，当前分支会前进一次，例如在temp提交一次后再次打印git log
#### git log -n2： (HEAD -> temp) 和 (master)两条提交信息，master不前进


### 7、比对两次提交的改变：git diff xxx xxx 
#### xxx可以根据 git log 打印出来的hash信息，
#### 也可以根据HEAD HEAD^1（上一级）HEAD^1^1（上两级）
#### git diff HEAD^1（之前的） HEAD（目前的）

### 8、删除分支操作：git branch -d xxx(分支名)
#### 有时候git会提示该分支没有merge的操作，确认删除此分支使用 -D

### 9、修改最近一次commit 的 message 信息：git commit --amend
#### 编辑第一行的message，esc退出编辑，:wq保存并退出

### 10、修改以前的commit （的 message） 信息： git rebase -i 要改的父亲的hash
#### 编辑第一行的 pick 为r（reword表示只改message），esc退出编辑，:wq保存并退出
#### 再次编辑 message，esc退出编辑，:wq保存并退出（:q!放弃修改并退出）

### 11、合并几次commit：git rebase -i 要合并的最前的commit的父的hash
####  编辑要合并的 commit 的前面为s


pick ddcb7ba save readme
s 49c58fc save readme 2
s 15eb7b7 change readme 3
pick acfb6cc change message



#### 第一行是为pick不变
#### 最后一行是最新也不变
#### 然后保存退出来到message继续编辑信息保存退出

### 注意 修改 commit(变基操作) 的操作比较适合在本地的自己的分支上面操作，
### 涉及他人或者远程分支的修改操作要谨慎

### 12、暂存区内容(已经git add)与当前HEAD作比较：git diff --cache

### 13、工作区与暂存区作比较：git diff （-- 文件名）


 







