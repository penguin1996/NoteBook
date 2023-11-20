```
查看release3是从哪个分支拉出来的

# 方式 1
git reflog --date=local | grep release3
5c50761 HEAD@{Thu Jun 29 12:53:45 2023}: checkout: moving from release2 to release3

# 方式 2
git reflog show release3
1ffdd7c (HEAD -> release3) release3@{0}: commit: update
17c9f82 release3@{1}: commit: update
00f6d6a release3@{2}: commit: update
5c50761 (origin/release1, origin/main, release2, release1, release, main) release3@{11}: branch: Created from HEAD

```

Git可以使用git reflog --date=local | grep +分支名来查看当前分支是从哪个分支拉下来的。

可以使用git log --graph --decorate --oneline --all来查看当前分支来查看是从哪个分支拉的。

用一个git branch这个比较万能的命令来查看当前分支是从哪个分支拉取的。