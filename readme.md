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

### 4、打开git图形化界面：gitk

### 5、git里面的三个对象：commit tree(文件数) blob(文件)

### 6、切换分支：git checkout -b 分支名xxx 基于哪个分支xxx
#### 例如 基于 master 创建 temp : git checkout -b temp master
#### git log -n1 可以看到 最新的提交信息里面 (HEAD -> temp, master)
#### 每一次提交，当前分支会前进一次，例如在temp提交一次后再次打印git log
#### git log -n2： (HEAD -> temp) 和 (master)两条提交信息，master不前进


### 7、比对两次提交的改变：git diff xxx xxx 
#### xxx可以根据 git log 打印出来的hash信息，
#### 也可以根据HEAD HEAD^1（上一级）HEAD^1^1（上两级）
#### git diff HEAD^1 HEAD（目前的）








