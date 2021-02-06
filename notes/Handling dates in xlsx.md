# Handling dates in xlsx
---
- author: #alex
---

```
var wb = XLSX.readFile(".tmp/uploads/"+file_name.split('_').join('.'),{cellDates: true });
```

Read the file with `cellDates` set at true. 


ref: https://stackoverflow.com/a/50823222