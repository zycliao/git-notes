## 基本概念
版本（commit）
本地目录/工作区（working tree）
缓冲区（index file）
HEAD：当前版本，实际上是一个指针，指向某一版本
分支（branch）：实际上也是一个指针

## 准备
### 配置
```
git config --global user.name <username>
git config --global user.email <email>
```
### 创建自己的仓库
```
git init 
```
在项目根目录下输入
## 基本操作
### 提交commit
```
git add  # 将未在index或modified过的文件添加至index
git commit [-m <注释>]  # 清空index，新建commit
git commit -a  # 相当于自动add modified过的文件然后commit
```
### 移除文件
```
git rm
```
删除文件，并将删除文件的信息添加到缓存区，commit后本地仓库的文件才会删除，本地文件不会改变
### 查看状态
```
git ls-files  # 查看有哪些文件处于版本控制状态
git status  # 查看当前状态
git log --graph --oneline  # 使用图形界面查看版本变更情况
```
### 比较状态
```
git diff  # 比较working tree与index
git diff --cached  # 比较HEAD与index
git diff <commit>  # 比较working tree与某个commit
git diff --cached <commit>  # 比较index与某个commit
git diff <commit1> <commit2>  # 比较两个commit
git diff [...] <path>  # 之比较path中的文件，...为上述参数
```

## Git中的换行符
LF（0x0a）为UNIX中换行符，CRLF（0x0d0a）为windows中的换行符
```
git config --global core.autocrlf true  # 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf input  # 提交时转换为LF，检出时不转换
git config --global core.autocrlf false  # 提交检出均不转换
git config --global core.safecrlf true  # 拒绝提交包含混合换行符的文件
git config --global core.safecrlf false  # 允许提交包含混合换行符的文件
git config --global core.safecrlf warn  # 提交包含混合换行符的文件时给出警告
```
一般来说，可使用
```
git config --global core.autocrlf false
git config --global core.safecrlf true
```
然后使用本地IDE手动统一换行符