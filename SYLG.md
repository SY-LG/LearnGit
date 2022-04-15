---
CJKmainfont: SimSun
toc: true
toc-title: "目录"
toc-own-page: true
author: "SYLG"
title: "SYLG Learning Git"
---

# something to say

## about this git repo

在看了[$\underline{\text{廖老师的git教程}}$](https://www.liaoxuefeng.com/wiki/896043488029600#0)后，我已经对git的使用有了基础的了解。但是，廖老师的教程面向初学者，并没有覆盖所有的方面，而网上的帖子说法又含糊不清（看官方文档太累了QAQ），因此，我便创建了这个git仓库，从个人的使用需求角度来进行实践以及记录。

## about this document

写这个文档目的有三：一者，一位好朋友想和我交流一些git方面的知识，而这个文档是一个不错的媒介；二者，这个文档也可以算进社团的文档产出里头；另外，我还想顺便试一试[$\underline{\text{这个markdown模板}}$](https://github.com/Wandmalfarbe/pandoc-latex-template)。

## syntax

这个文档里会包含许许多多命令行操作，它们会以代码块的格式出现：

```
user MINGW64 ~/LearnGit (master)
$ git --version
git version 2.35.1.windows.2
```

第一行是关于用户名、git bash工作目录等的基本信息。若不发生变化，一个代码块中只会保留一行。作为隐私，我的用户名一律取代为user；涉及用户目录路径的，我会以~进行部分替代。（下文中涉及隐私替代的都会在这里进行补充）

“$”符号后面的是输入的命令，其余为git的反馈。git命令成功执行时往往没有反馈，仅以空行隔开。在代码块中我将省略这样的空行。

上文的命令能输出我当前的git版本。下文的所有命令全部基于这个版本的git进行，若您的git版本与我的差异较大，可能要留意某些命令的区别。

另外，为了区分这个文档的更改以及对git的探索，我会在commit message里面以\[doc\]和\[git\]进行标注。

最后，您可能会留意到这个文档的标题都是英文。这并不是因为我有多想展示我那拙劣的英文水平，而是因为pandoc和上文提到的markdown模板对中文的支持比较弱，以中文作为标题会影响美观性。因此，还请您多多容忍这篇文档中英文部分的各种不恰当、不妥帖。

# basic usage

这部分涉及的命令比较基础，廖老师在他的教程里面也阐述得比较完备，因此解释性语言会比较少。

## init

```
user MINGW64 ~/LearnGit (master)
$ git init
Initialized empty Git repository in ~/LearnGit/.git/
```

## add and commit

```
user MINGW64 ~/LearnGit (master)
$ git add SYLG.md
$ git add .gitignore
$ git commit -m "[doc] as a start"
[master (root-commit) a6590cd] [doc] as a start
 2 files changed, 49 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 SYLG.md
```

git add可以通过"git add ."命令（本质上是正则匹配）将所有有改动的文件添加到暂存区。现在的.gitignore文件里面只有一行：\*.pdf，用以忽略这个文档导出的pdf格式文件。

## add remote repo

```
user MINGW64 ~/LearnGit (master)
$ git remote add origin git@github.com:SY-LG/LearnGit.git
$ git branch -M main
user MINGW64 ~/LearnGit (main)
$ git push -u origin main
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 1.78 KiB | 364.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:SY-LG/LearnGit.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

## reset

```
user MINGW64 ~/LearnGit (main)
$ git reset --hard HEAD^^
HEAD is now at a6590cd [doc] as a start
```

将版本回退至两次提交之前。HEAD^^指代该次提交，表达同样意义的还有HEAD~2或该次提交的commit id

```
user MINGW64 ~/LearnGit (main)
$ git reflog
a6590cd (HEAD -> main) HEAD@{0}: reset: moving to HEAD^^
42d5995 HEAD@{1}: commit: [doc] change metadata block
14e68e5 (origin/main) HEAD@{2}: commit: [doc] add add-and-commit and add-remote-repo
a6590cd (HEAD -> main) HEAD@{3}: Branch: renamed refs/heads/master to refs/heads/main
a6590cd (HEAD -> main) HEAD@{5}: commit (initial): [doc] as a start
$ git reset --hard 42d5
HEAD is now at 42d5995 [doc] change metadata block
```

通过查看所有命令的记录找到想要恢复的版本的commit id并恢复到版本回退之前