# 和 remote 相关

第二步：使用下述命令查看 remote 地址，远程分支，还有本地分支与之对应的关系等信息

```bash
git remote show origin
```

![](https://i-blog.csdnimg.cn/blog_migrate/fe4c2d716bfb55aad5b63b1084b358c1.png)  

第三步：使用下述命令在本地删除远程不存在的分支

```bash
git remote prune origin
```

## ****用两行命令删除分支****

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

# 本地仓库和工作区的内容 diff

你可以使用以下命令查看上次提交之后的文件修改和具体修改内容：

1. 查看修改的文件：

   ```bash
   git diff --name-only HEAD
   ```

2. 查看具体的修改内容：

   ```bash
   git diff HEAD
   ```

- 第一个命令 `git diff --name-only HEAD` 会列出自上次提交以来被修改的文件名。
- 第二个命令 `git diff HEAD` 会显示这些文件的具体修改内容，包括新增、删除和修改的行。
