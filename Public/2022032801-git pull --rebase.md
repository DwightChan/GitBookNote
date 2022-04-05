[toc]

---

# [聊下git pull --rebase](https://www.cnblogs.com/wangiqngpei557/p/6056624.html)

官方介绍 
> 官方链接 https://www.gitkraken.com/learn/git/problems/git-pull-rebase

# [简单对比git pull和git pull --rebase的使用](https://www.cnblogs.com/kevingrace/p/5896706.html)

 

使用下面的关系区别这两个操作：
git pull = git fetch + git merge
git pull --rebase = git fetch + git rebase

现在来看看git merge和git rebase的区别。

假设有3次提交A,B,C。

![img](https://images2015.cnblogs.com/blog/907596/201609/907596-20160922155014777-999552544.png)

在远程分支origin的基础上创建一个名为"mywork"的分支并提交了，同时有其他人在"origin"上做了一些修改并提交了。

![img](https://images2015.cnblogs.com/blog/907596/201609/907596-20160922155038152-1733703139.png)

其实这个时候E不应该提交，因为提交后会发生冲突。如何解决这些冲突呢？有以下两种方法：

1、git merge
用git pull命令把"origin"分支上的修改pull下来与本地提交合并（merge）成版本M，但这样会形成图中的菱形，让人很困惑。

![img](https://images2015.cnblogs.com/blog/907596/201609/907596-20160922155107949-1520786903.png)

2、git rebase
创建一个新的提交R，R的文件内容和上面M的一样，但我们将E提交废除，当它不存在（图中用虚线表示）。由于这种删除，小李不应该push其他的repository.rebase的好处是避免了菱形的产生，保持提交曲线为直线，让大家易于理解。

![img](https://images2015.cnblogs.com/blog/907596/201609/907596-20160922155132715-596060966.png)

在rebase的过程中，有时也会有conflict，这时Git会停止rebase并让用户去解决冲突，解决完冲突后，用git add命令去更新这些内容，然后不用执行git-commit,直接执行git rebase --continue,这样git会继续apply余下的补丁。
在任何时候，都可以用git rebase --abort参数来终止rebase的行动，并且mywork分支会回到rebase开始前的状态。

*************** 当你发现自己的才华撑不起野心时，就请安静下来学习吧！***************
