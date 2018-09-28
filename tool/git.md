### git取消最近一次commit

```javascript
$ git commit -m "Something"            
$ git reset HEAD~                                          
```

然后做新的`commit`

```javascript
$ git add ...                                              
$ git commit -c ORIG_HEAD 
```