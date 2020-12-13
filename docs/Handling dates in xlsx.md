# Handling dates in xlsx
---
- keywords: [[npm xlsx]], [[How to get things done with switchless]]
- author: [[Alex]]
---

```
var wb = XLSX.readFile(".tmp/uploads/"+file_name.split('_').join('.'),{cellDates: true });
```

Read the file with `cellDates` set at true. 


ref: https://stackoverflow.com/a/50823222