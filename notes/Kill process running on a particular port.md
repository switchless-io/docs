
# Kill process running on a particular port
---
- author: #alex 
---

```
lsof -i tcp:1001
```

```
lsof -ti tcp:1001 | xargs kill
```

https://til.hashrocket.com/posts/e4c8c665a8-find-and-kill-all-processes-listening-on-a-port