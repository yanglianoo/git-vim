# Git使用笔记

- git把本次修改的内容添加到上次提交中

```bash
git commit --amend #会通过 core.editor 指定的编辑器进行编辑
git commit --amend --no-edit #不会进入编辑器，直接进行提交
//可以配置vim位默认编辑器
git config --global core.editor /usr/bin/vim
```

- git撤销文件的修改

```bash
#1.在工作区修改，但并未提交到暂存区（即并没有add）。
#对于单个文件的撤销修改
git checkout -- 文件名
#撤销所有文件的修改
git checkout .
```

- git切换到某个commit ID

```bash
#查看所有提交
git log
#切换到某个commit
git checkout 22dfbf1f907764c5ae70381b8191104f9af21d8c #commit号
```

- git提交代码时出现Everything up-to-date的解决办法

```bash
1. 创建一个新的分支：git branch newBranch
2. 查看分支是否创建成功：git branch
3  切换到此分支：git checkout newBranch
4. 把代码直接提到newBranch分支上，如果出现以下提示：
5.切换（如：git checkout master）到原本想要提交代码的分支，把newBranch合并到master分支上：git merge newBranch
6.合并之后如果发现有冲突，可git diff查看有冲突的文件      ------ps：基本不会有冲突
7.最后就可以重新提交一下代码了，直接git push就可
原文链接：https://blog.csdn.net/zhuhongyang_/article/details/118521264
```
 - git 创建`gitignore`文件
```git
    <!-- 直接在项目目录下 touch .gitignore -->
    git rm -r --cached .    #新增的忽略文件没有生效，是因为git是有缓存的，而之前的文件在缓存中，并不会清除掉，还会继续提交，所以更新.gitignore文件，要清除缓存文件
    git add .
    git commit -m 'update .gitignore'
    git push origin master
```
 - `git stash`: 保存工作现场，即可切换到其他分之开发
 - `git stash pop`: 弹出暂存的更改，继续开发，恢复的同时把stash内容也删了
 - `git stash list`: 查看被statsh的内容
 - `git stash drop`: 删除stash的内容   
 