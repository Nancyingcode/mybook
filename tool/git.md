# git配置
```javascript
$ git config --global user.name "username"
$ git config --global user.email "name@example.com"

设置密码
ssh-keygen -t rsa -C "name@example.com"

把ssh目录下.pub后缀的内容添加到github

建立仓库
git init
git add README.md
git commit -m "commit message"
git remote add origin git@github.com:GithubName/project.git
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

>	`git`提交前如果要更新`pull`
>	先`git stash`将改变暂存
>	pull完成后再用`git stash pop`将内容合并
>	然后就可以`git push`


# git搭建个人服务器

在linux系统下 添加一个用户 git(可取其他名)
```javascript
sudo adduser git
```
然后选择你要建立仓库的地区 示例为 /home/git/pro
```javascirpt
sudo git init --bare /home/git/pro/pro.git
```
设置 仓库的权限为刚刚添加的git用户
```javascript
sudo chown -R git:git /home/git/pro/pro.git
```
限制其他用户通过shell登录服务器
```javascript
sudo vim /etc/passwd
```
修改
```javascript
git:x:1000:1000:nancyingRes,10,13129585774,none:/home/git:/bin/bash
```
为
```javascript
git:x:1000:1000:nancyingRes,10,13129585774,none:/home/git:/usr/bin/git-shell
```

clone
```javascript
git clone git@server:/home/git/prop/pro.git
```
`push`同理

