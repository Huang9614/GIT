# [interactive tutorial](https://learngitbranching.js.org/)

## operations on local repo.
```
git commit # 创建新节点
git branch + git checkout = git checkout -b <branch_name> # 创建分支并且切换到该分支


# 分支合并
git merge bugFix # 在main分支上进行
git rebase main # 在bugFix分支上进行


# 提交树上前后移动的方法
git checkout <branch-name> # 直接移动 HEAD 指向分支名或者指向具体的提交记录
git checkout <commit-history> # 此时HEAD和分支名分离
git checkout main^ # 相对移动 HEAD, 移动HEAD到main的上一个节点
git checkout HEAD^ # 移动HEAD到HEAD当前指向的节点的上一个节点
git checkout HEAD~4 # 移动HEAD到HEAD当前指向节点的前面第四个节点
git branch -f main HEAD~3 # 强制要求main指向HEAD指向的节点的前第3个节点


# 撤销变更
git reset # 仅面向local branch；被reset的提交记录仍然存在，但是处于为加入暂存区的状态
git reset HEAD^ # 当HEAD指向main时，该操作将main分支移回到前一个提交节点
git revert # 撤销更改并且分享
git revert HEAD # 当HEAD指向main时，该操作将创建新节点，该节点内容与前一个节点内容一致，增加了撤销变更的信息，并且将main移动到新节点

```

## operations on remote repo.

```
git clone <remote-repo>


o/main  # 远程分支, 命名规范 <remote_name>/<branch_name>; git clone时，自动将远程仓库命名为origin
        # 自动进入分离HEAD状态，即，即使是切换到了o/main，并且commit，也只有HEAD会发生移动；但是如果切换到local branch，就和之前一样了


git fetch # 获取远程提交记录，更新远程分支指针（origin/main）, 不修改本地文件和本地指针


# 合并远程分支中的更新
git rebase o/main
git merge o/main
git fetch + git merge o/main  = git pull # 先抓取再更新


# 上传更新
git push # 自动将本地的远程分支指针更新
## 当远程仓库发生了变动后，基于旧版本的更新无法直接push, 3 solvers:
git fetch + git rebase o/main + git push
git fetch + git merge o/main + git push
git pull  - - rebase + git push


# 远程服务器拒绝（remote rejected）： main分支被锁定，需要pull request流程合并修改
# 新建分支，然后后reset main，从而保持和远程服务器一致


# 远程跟踪分支: 让本地main分支追踪o/main对应的远程mian分支
git checkout -b totallyNotMain o/main 
git branch -u o/main foo # 要求foo分支，追踪o/main对应的远程main分支，如果当前在foo分支上，foo可以省去
```
