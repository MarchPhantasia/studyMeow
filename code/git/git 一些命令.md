第二步：使用下述命令查看remote地址，远程分支，还有本地分支与之对应的关系等信息

```bash
git remote show origin
```

![](https://i-blog.csdnimg.cn/blog_migrate/fe4c2d716bfb55aad5b63b1084b358c1.png)  

第三步：使用下述命令在本地删除远程不存在的分支

```bash
git remote prune origin
```

### ****用两行命令删除分支****

```bash
// 删除本地分支
git branch -d localBranchName

// 删除远程分支
git push origin --delete remoteBranchName
```

使用以下命令同步分支列表：

```
git fetch -p
```