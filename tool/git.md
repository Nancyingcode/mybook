# git配置
```javascript
$ git config --global user.name "username"
$ git config --global user.email "name@example.com"

ssh-keygen -t rsa -C "name@example.com"

git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:Nancyingcode/java-template.git
git push -u origin master
```
# git取消最近一次commit`

```javascript
$ git commit -m "Something"            
$ git reset HEAD~                                          
```

然后做新的`commit`

```javascript
$ git add ...                                              
$ git commit -c ORIG_HEAD 
```
# git stash
	`git`提交前如果要更新`pull`
	先`git stash`将改变暂存
	pull完成后再用`git stash pop`将内容合并
	然后就可以`git push`

