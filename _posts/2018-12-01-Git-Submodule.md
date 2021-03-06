---
layout:     post                    # 使用的布局（不需要改）
title:      Git Submodule           # 标题 
subtitle:                           #副标题
date:       2018-12-01              # 时间
author:     smy                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Git
---

当一个项目需要包含其他支持项目源码时使用的功能，作用是两个项目是独立的，且主项目可以使用另一个支持项目。

```
$ git submodule add <submodule_url>   # 添加子项目
  ex: git submodule add git@gitlab.com:stardust.ai/shared_models.git
```

> 添加子项目后会出现.gitmodules的文件，这是一个配置文件，记录mapping between the project's URL and the local subdirectory。且.gitmodules在git版本控制中，这样其他参与项目的人才能知道submodule projects的情况。

```
$ git submodule init  # 初始化本地.gitmodules文件
```

```
$ git submodule update  # 同步远端submodule源码
```

> 如果获取的项目包含submodules，pull main project的时候不会同时获取submodules的源码，需要执行本地.gitmodules初始化的命令，再同步远端submodule源码。如果希望clone main project的时候包含所有submodules，可以使用下面的命令

```
$ git clone --recurse-submodules <main_project_url>
```

* 获取主项目和所有子项目源码
操作submodules源码：先进入submodule的direcotry，再执行下述命令

```
$ git fetch  # 获取submodule远端源码

$ git merge origin/<branch_name>  # 合并submodule远端源码

$ git pull  # 获取submodule远端源码合并到当前分支

$ git checkout <branch_name>  # 切换submodule的branch

$ git commit -am "change_summary"  # 提交submodule的commit
```

## or

* 更新submodule源码，默认更新的branch是master，如果要修改branch，在.gitmodule中设置
```
$ git submodule update --remote <submodule_name>  
```

* 更新所有submodule源码，默认更新.gitmodule中设置的跟踪分支，未设置则跟踪master
``` 
$ git submodule update --remote  
```

* 当submodule commits提交有问题的时候放弃整个push
```
$ git push --recurse-submodules=check
```

* 分开提交submodule和main project
```
$ git push --recurse-submodules=on-demand
```

* .gitmodule内容大致如下
```md
[submodule <submodule_name>]
    path = <local_directory>
    url = <remote_url>
    branch = <remote_update_branch_name>
```

* 用'foreach'关键字同时管理多个submodules，如下

* stash所有submodules
```
$ git submodule foreach 'git stash'
```

* 所有submodules创建新分支
```
$ git submodule foreach 'git checkout -b <branch_name>'
```

* submodules的命令很长，为提升效率，可以创建alias，记录在.git/config路径下。如下：
```
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge'
```

这样，可以使用下面的命令来提高效率
```
$ git supdate
$ git spush
```

一次性Clone项目和Submodules
```
$ git clone --recursive /path/to/repos/foo.git
```

移除submodule
```
1、删除git cache和物理文件夹
$ git rm -r --cached libs/
$ rm -rf libs

2、删除.gitmodules的内容（或者整个文件）
$ rm .gitmodules

如果仅仅删除某一个submodule那么打开.gitmodules文件编辑，删除对应submodule配置即可。

3、删除.git/config的submodule配置

源文件：
<pre>[core]
    repositoryformatversion = 0 
    filemode = true
    bare = false
    logallrefupdates = true
[remote "origin"]
    fetch = +refs/heads/*:refs/remotes/origin/*
    url = /home/henryyan/submd/ws/../repos/project1.git
[branch "master"]
    remote = origin
    merge = refs/heads/master
[submodule "libs/lib1"]
    url = /home/henryyan/submd/repos/lib1.git
[submodule "libs/lib2"]
    url = /home/henryyan/submd/repos/lib2.git
</pre>
 
删除后：
<pre>[core]
    repositoryformatversion = 0 
    filemode = true
    bare = false
    logallrefupdates = true
[remote "origin"]
    fetch = +refs/heads/*:refs/remotes/origin/*
    url = /home/henryyan/submd/ws/../repos/project1.git
[branch "master"]
    remote = origin
    merge = refs/heads/master
</pre>
```