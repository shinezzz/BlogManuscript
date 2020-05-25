# git

1. git日志:`git --oneline --graph`
2. 比较两次commit的不同`git diff commit1 commit2`
3. 删除分支:`git branch -d branch1`或者`git branch -D branch2`
4. 修改最新的commit信息:`git commit --amend`
5. 修改老旧的commit信息:`git rebase -i 父亲Hash` and `r`
6. 连续多个commit整合成一个:`git rebase -i 最早Hash` and `s`
7. 间隔多个commit整合成一个:`git rebase -i 祖宗Hash` and `s`
8. 比较暂存区和HEAD文件差异:`git diff --cached`
9. 暂存区恢复成HEAD:`git reset HEAD`
10. 工作区恢复为暂存区:`git checkout -- <file>`
11. 取消暂存区部分的更改:`git reset HEAD <file>`
12. 消除最近的几次提交:`git reset --hard commitHash`
13. 不同提交指定文件的差异:`git diff masterHash tempHash -- <file>`
14. 正确删除文件:`git rm <file>`
15. 紧急任务:`git stash`  and `git stash apply`
16. 文件.gitignore

    语法规范

    - 空行或是以#开头的行即注释行将被忽略。
    - 可以在前面添加正斜杠/来避免递归,下面的例子中可以很明白的看出来与下一条的区别。
    - 可以在后面添加正斜杠/来忽略文件夹，例如build/即忽略build文件夹。
    - 可以使用!来否定忽略，即比如在前面用了*.apk，然后使用!a.apk，则这个a.apk不会被忽略。
    - \*用来匹配零个或多个字符，如\*.\[oa\]忽略所有以".o"或".a"结尾，*~忽略所有以~结尾的文件（这种文件通常被许多编辑器标记为临时文件）；\[\]用- 来匹配括号内的任一字符，如\[abc\]，也可以在括号内加连接符，如\[0-9\]匹配0至9的数；?用来匹配单个字符。

        ```bash
        # 忽略 .a 文件
        *.a
        # 但否定忽略 lib.a, 尽管已经在前面忽略了 .a 文件
        !lib.a
        # 仅在当前目录下忽略 TODO 文件， 但不包括子目录下的 subdir/TODO
        /TODO
        # 忽略 build/ 文件夹下的所有文件
        build/
        # 忽略 doc/notes.txt, 不包括 doc/server/arch.txt
        doc/*.txt
        # 忽略所有的 .pdf 文件 在 doc/ directory 下的
        doc/**/*.pdf
        ```
