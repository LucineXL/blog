---
title: githug
date: 2020-03-10 17:29:30
tags:
    - git
    - githug
cover: https://images.pexels.com/photos/3756659/pexels-photo-3756659.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
---


githug 是一个可以快速熟悉git基本命令的一个小游戏, 初学者可以通过这个小游戏快速上手git

[github链接戳这里][0]

### 1. init


> Name: init
Level: 1
Difficulty: *

> A new directory, `git_hug`, has been created; initialize an empty repository in it.
 新的目录git_hug已经创建； 在其中初始化一个空的存储库。


初始化一个Git仓库， 命令：
`git init `

该命令将创建一个名为 .git 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。
.git 是一个隐藏文件， 可以使用 `ls -a` 查看

![image.png](https://upload-images.jianshu.io/upload_images/5723572-14ff091c88b5d9c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 2. config

> Name: config
Level: 2
Difficulty: *

> Set up your git name and email, this is important so that your commits can be identified.
 设置您的git名称和电子邮件，这一点很重要，以便可以识别您的提交。


设置用户名和邮箱地址之后，以后每一次提交都会使用设置的用户信息， 这样可以方便以后查找代码是谁提交的

```
git config --global user.name "name" // 设置名称
git config --global user.email "email"  // 设置邮箱
git config user.name // 查看名称
git config user.email // 查看邮箱

```

使用`git config -l` 可以查看所有的用户配置


### 3. add

> Name: add
Level: 3
Difficulty: *

> There is a file in your folder called `README`, you should add it to your staging area
Note: You start each level with a new repo. Don't look for files from the previous one.
文件夹中有一个名为“ README”的文件，应将其添加到暂存区中
注意：您可以从一个新的仓库开始每个级别。 不要查找上一个文件。

<br/>
在git中， 分为三个区： 工作区， 暂存区 和 版本库

1. 工作区： 我们直接编辑的地方
2. 暂存区： 数据暂时存放的地方， 可用于工作区和版本库之间的交流
3. 版本库： 存放已经提交的数据

三个区之间的关系： (此图来自[https://blog.csdn.net/qq_32452623/article/details/78417609][1])
![](https://raw.githubusercontent.com/DRPrincess/BlogImages/master/qiniu/2429e4d2661e60027537aea0077f6e40.png)

`git add` 命令的作用就是讲本地工作区的内容添加至暂存区


```
git add -A     提交所有修改
git add .      提交新文件和被修改文件，不包括被删除文件
git add -u     提交被修改和被删除文件，不包括新文件
```

所以本题使用上述三个命令均可

### 4.commit

> Name: commit
Level: 4
Difficulty: *

> The `README` file has been added to your staging area, now commit it.
`README`文件已添加到您的暂存区，现在提交。


```
git commit -m '我是提交文案'
```

### 5. clone

> Name: clone
Level: 5
Difficulty: *

> Clone the repository at https://github.com/Gazler/cloneme.
克隆存储库，网址为https://github.com/Gazler/cloneme。

我们在进行开发时， 需要把远程仓库克隆到本地， 在本地进行开发， 就可以使用 `git clone` 命令，

```
git clone https://github.com/Gazler/cloneme
```

这样会将 https://github.com/Gazler/cloneme 这个远程仓库克隆至当前文件夹， 名称为 cloneme


### 6. clone_to_folder

> Name: clone_to_folder
Level: 6
Difficulty: *

> Clone the repository at https://github.com/Gazler/cloneme to `my_cloned_repo`.
将位于https://github.com/Gazler/cloneme的存储库克隆到`my_cloned_repo`。

```
git clone https://github.com/Gazler/cloneme my_cloned_repo
```
将远程仓库克隆到某一特定文件夹， 直接在仓库地址后面添加文件夹名称即可。

### 7. ignore

> Name: ignore
Level: 7
Difficulty: **

> The text editor 'vim' creates files ending in `.swp` (swap files) for all files that are currently open.  We don't want them creeping into the repository.  Make this repository ignore those swap files which are ending in `.swp`.
文本编辑器'vim'为当前打开的所有文件创建以`.swp`结尾的文件（交换文件）。 我们不希望它们爬行到存储库中。 使此存储库忽略那些以`.swp`结尾的交换文件。

.ignore 文件放在项目的根目录下， 用来配置可忽略文件

![image.png](https://upload-images.jianshu.io/upload_images/5723572-6b352cbcefec2da7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 8. include

>Name: include
Level: 8
Difficulty: **

>Notice a few files with the '.a' extension.  We want git to ignore all but the 'lib.a' file.
注意一些扩展名为“ .a”的文件, 我们希望git忽略所有除'lib.a'外所有'.a'的文件。

如图：

![image.png](https://upload-images.jianshu.io/upload_images/5723572-42a50d4c727193c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 9. status

>Name: status
Level: 9
Difficulty: *

>There are some files in this repository, one of the files is untracked, which file is it?
此存储库中有一些文件，其中一个文件未跟踪，它是哪个文件？

使用 `git status` 命令可以查看文件的状态， 如下图

![image.png](https://upload-images.jianshu.io/upload_images/5723572-e1984310fceb2263.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


还可以使用 `git status -s ` 查看简写状态。
在简写状态下一般用到的几种情况：  `M - 被修改，A - 被添加，D - 被删除，R - 重命名，?? - 未被跟踪 `

![image.png](https://upload-images.jianshu.io/upload_images/5723572-986c6270b0acc03c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 10. number_of_files_committed

>Name: number_of_files_committed
Level: 10
Difficulty: *

>There are some files in this repository, how many of the files will be committed?
此存储库中有一些文件，将提交多少个文件？

这个题目还是可以使用 `git status` 进行查看， 但是注意的是， 只有已经被暂存过的文件才会被提交哦

![image.png](https://upload-images.jianshu.io/upload_images/5723572-c3e9d7d7ea0af181.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 11. rm

>Name: rm
Level: 11
Difficulty: **

>A file has been removed from the working tree, however the file was not removed from the repository.  Find out what this file was and remove it.
文件已从工作树中删除，但是该文件未从存储库中删除。 找出此文件是什么并将其删除。

`git rm` 可以同时从工作区和索引中删除文件， 删除后，git将不会继续追踪到该文件, 效果有点类似 `.gitignore`文件. 但是 一个文件如果已经存在在远程仓库， 设置 `.gitignore` 后将不会生效， 此时可以通过 `git rm` 将该文件移除

![](https://tva1.sinaimg.cn/large/00831rSTly1gdmgpfl62kj30pq0esjtz.jpg)







 [0]: https://github.com/Gazler/githug
 [1]: https://blog.csdn.net/qq_32452623/article/details/78417609