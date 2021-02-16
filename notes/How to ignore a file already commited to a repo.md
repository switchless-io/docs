# How to ignore a file already commited to a repo

Add it to `.gitignore`

```
.obsidian/workspace
.obsidian/graph.json
```

Ask git to not track this file by removing it from its index
```shell
git rm --cached .obsidian/workspace
```

Now `git status` will show that you have deleted the file. 

Go ahead and commit the new `.gitignore` and the deleted file.

ref: https://gist.github.com/tsrivishnu/a2f3adbbca9fcad5f3597af301ad1abb