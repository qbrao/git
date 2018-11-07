# git

## 参考资料

- [Git飞行规则](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md)

## 分支

以前都是在 dev 上开发，这段时间由于项目频繁发版，所以考虑在新的 feature 分支上开发新功能，网上搜了一些资料，现在记录一下整个流程。

假设远程仓库已经有 `master` 和 `dev` 两个分支。

进入 dev 分支

```sh
git checkout dev
```

基于 dev 分支创建新分支 `feature/A`。新开发的功能以 `feature` 开头，`A` 为功能名称，作为命名规范。

```sh
git branch feature/A
```

切换到 `feature/A` 分支

注意这里还是本地分支，使用 `git branch` 查看本地分支， 会显示 `feature/A` 和 `dev` 两个分支。分支前面有 `*` 代表是当前分支。

使用 `git branch -r` 查看远程分支是没有 `feature/A` 分支的。

```sh
git checkout feature/A
```

把 `feature/A` 分支推送到远程仓库。然后使用 `git branch -r` 查看远程分支， `feature/A` 分支已经存在。

注意：远程分支和本地分支的名称要保持一致。

```sh
git push origin develop
```

完成功能后需要删除本地和远程分支。先用 `git branch -a` 来查看所有分支，包括本地和远程分支。

删除本地分支
```sh
git branch -d feature/A
```

删除远程分支

```sh
git push origin --delete feature/A
```

现在有个问题，在 `dev` 分支上面修复了 bug （本来应该新建一个分支来修复bug，现在暂时不考虑，直接在 `dev` 上修复），如何把 `dev` 分支修复后的代码合并到 `feature/A` 分支上？

- 第一步：切换到 `feature/A` 分支；
- 第二步：合并分支 `git merge dev`；
- 完成。

`pull` 或者 `merge` 分支时，有时候会遇到这个界面，如下图：

![img](./images/merge-error.jpg)

可以不管(直接下面3,4步)，如果要输入解释的话就需要:

1. 按键盘字母 `i` 进入 insert 模式。
2. 修改最上面那行黄色合并信息,可以不修改。
3. 按键盘左上角 `Esc`。
4. 输入 `:wq`，回车。

git push origin :fromdevelop   //删除远程fromdevelop分支

$ git branch -d <BranchName>      // 删除本地分支 

## 回滚

今天 pull 代码后，打包出现问题，但是找不到出问题的具体文件。使用排除法来查找具体是哪次提交的问题。
先查看提交的 log，按字母 q 可以退出日志模式。

```sh
git log
```

回滚到具体的某个版本

```sh
git reset --hard e377f60e28c8b84158
```

强制提交

```sh
git push -f origin master
```