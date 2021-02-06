# Gitignore for obsidian

if you are going to use git to version control your obsidian project, then add these to gitignore

```
/.obsidian/workspace
.obsidian/workspace
.obsidian/graph.json
```


Here the entire obsidian folder is not skipped. This is because you might want your config to be also version controlled. This might be an issue if another person who is also contributing prefers a different config. The second person can always choose to make changes to his/her config locally and not commit it. 