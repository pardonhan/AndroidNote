## git-svn 操作的一些记录


### 将现有git项目提交到svn库

1.有svn空库

2.有git版本库

3.在.git/config中添加svn-remote

```
	[svn-remote "svn"]
	     url = http://svn.example.com/foo/trunk
	     fetch = :refs/remotes/git-svn
```

4.从空的svn远程库中做初始化fetch,并将其作为一个新分支checkout

```
	git svn fetch svn  
	git checkout -b svn git-svn
```

5.将master分支merge进svn分支并提交到svn库

```
	git merge master
	git svn dcommit
```

6.rebase到svn分支以便从master版本推送到svn库

```
	git checkout master
	git rebase svn
	git branch -d svn

```