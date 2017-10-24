## 克隆远程库
```
git clone <远程地址> <本地目录名>
```
## 创建ssh连接
在用户主目录下有.ssh目录，下面有`id_rsa`和`id_rsa.pub`，分别是私钥和公钥  
如果没有这两个文件，可用
```
ssh-keygen -t rsa -C "youremail@example.com"
```
来创建

## 远程仓库
### 关联远程仓库
```
git remote add origin git@github.com:username/repo.git  # origin代表远程库的名字
# 这个库也可以是本地的，比如
git remote add myrepo /temp/myrepo
```
### 追踪远程仓库的分支
```
git branch --set-upstream <本地分支> <远程主机>/<远程分支>
```
在建立了分支追踪后，pull和push操作可省略远程分支名

### 查看/编辑远程仓库
```
git remote  # 查看关联的远程仓库
git remote -v  # 查看远程仓库主机的地址
git remote show <主机名>  # 查看主机详细信息
git remote rename <原主机名> <新主机名>  # 重命名
git remote rm origin  # 取消关联
```
若使用git clone从远程仓库复制，会自动关联，并命名为origin

## 远程拉至本地
### fetch
```
git fetch <远程主机名> <分支名>  # 若不加分支则fetch所有分支
```
fetch是将远程分支复制一份到本地，并在本地命名为 <远程主机名>/<分支名>，git branch无法查看，需加参数-r（显示远程分支）或-a（显示所有分支

### pull
pull等同于fetch+merge
```
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull --rebase <远程主机名> <远程分支名>:<本地分支名>  # pull将等同于fetch+rebase
```
若不加本地分支名则默认与当前分支合并；  
若不加远程分支名，则默认与本地分支追踪的远程主机分支合并；   
若只有一个远程主机并建立了追踪关系，则可省略远程主机名  

## 本地推至远程
```
git push <远程主机名> <本地分支名>:<远程分支名>  # 如果远程分支不存在，则会被自动创建
git push <远程主机名> :<远程分支名>  # 删除远程分支，相对于push了一个空分支
git push <远程主机名>  # 若当前本地分支与远程分支存在追踪，则可省略分支名
git push  # 只存在一个远程主机并追踪了分支可用该命令，若有多个远程主机则推至默认主机
git push -u <远程主机名> <本地分支名>  # 会自动与远程的与本地分支同名的分支建立追踪（upstream），若远程无该分支，将新建之
git push --all <远程主机名>  # 推本地所有分支至远程
git push --force <远程主机名>  # 若远程仓库版本较新，要先pull再push，加force可强制覆盖 
```