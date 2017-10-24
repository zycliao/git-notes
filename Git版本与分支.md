## 版本穿梭
```
git reset --hard <版本>  # 本地代码和缓冲区均reset
git reset --soft <版本>  # 本地代码和缓冲区均不reset
git reset --mixed <版本>  # 缓冲区reset，本地代码不reset
```
其中版本可为HEAD指针，HEAD表示当前版本，HEAD^表示前一版本，HEAD~n表示前n版本  
HEAD也可用版本号代替，版本号为SHA1码，可用git log查看  
reset之后，git log无法查看该版本之后版本，若要查看未来版本号，可使用git reflog  
## 分支
### 分支的创建/编辑
```
git branch  # 查看当前所有分支，*号表示当前工作在哪个分支
git branch <新分支名> [<源分支>]  # 创建一个新分支并指向源分支，若不加源分支，则默认新分支指针指向当前分支（HEAD）
git branch -d <分支名>  # 删除，只能删除已经被当前分支合并的分支
git branch -D <分支名>  # 强制删除
git branch -m <旧分支> <新分支>  # 重命名分支，-M为强制
```
### 分支切换
```
git checkout <分支名>  # 切换到其他分支
git checkout -b <新分支名> [<源分支>]   # 创建并切换，相当于branch+checkout
```
### 分支合并
```
git merge -m <注释> <分支名a>  # 将分支a合并到当前分支
```
merge有若干种情况：  
1.两分支在同一分支，且分支a比当前分支的版本更新，merge将直接完成，提示Fast-forward，两分支将指向同一commit（a的最新版本），不产生新的commit  
2.两分支在同一分支，且当前分支比分支a的版本更新，提示Already up-to-date，不产生任何变化  
3.两分支不在同一分支，产生冲突，冲突文件将放在index中，需要手动解决后add并commit，产生一个新的commit（其注释信息为merge时的注释信息而非最后一次commit的），当前分支指向新的commit，分支a的指向不变，不过在版本图中分支a所指commit会与当前分支commit向连，表示其已被合并，可以安全将分支a删除  
### 分支文件操作
merge会将两分支完全合并，若只是想要合并部分文件，可用如下命令
```
git checkout <源分支> [--] <文件>  # 用源分支中的指定文件覆盖掉当前working tree的文件，并添加到index中
```
### rebase合并
```
git rebase <分支a>  # 开始rebase
git rebase --continue  # 继续rebase
git rebase --abort  # 终止rebase，将退回到开始之前状态
```
类似merge会产生3种情况：  
1.同merge  
2.同merge  
3.假设从C0起两分支分叉，通过C0-C1-C2-C3到当前分支，设A为分支a此时所在commit，  
在输入rebase后，A后将产生新commit C1'，为A与C1的merge，解决冲突后git add冲突文件，使用git rebase --continue继续，  
C1'后将产生新commit C2'，为C2与C1'的merge，解决冲突后继续，  
C2'后将产生新commit C3'，为C3与C2'的merge，解决冲突继续后将完成rebase  
此时当前分支指针指向C3'，分支a指针不变（扔指向A），C1,C2,C3将被抛弃，C1',C2',C3'的注释信息与C1,C2,C3相同  