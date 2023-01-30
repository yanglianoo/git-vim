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

