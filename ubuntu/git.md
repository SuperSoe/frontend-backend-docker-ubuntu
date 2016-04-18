git操作
=====
+ 先远端克隆项目
```　
git clone git@服务器地址://source/code/project.git
```
+ 合并种子项目到本项目

```
git remote add upstream git@192.168.1.201:/home/source/soesoft/soe-rest.git

git fetch upstream

git merge upstream/master

```

+ 本地切换到ｍａｓｔｅｒ分支 合并upstream/master


```
git checkout master
git merge upstream/master
```



+  查看远端分支

```
git branch -r

git checkout -b 本地分支　远端分支

git merge master
```