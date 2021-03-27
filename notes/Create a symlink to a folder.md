---
author:#alex
---
# Create a symlink to a folder

This is useful when you are modularising your code. part of your code is in a particular folder and you want to refer to this code base in another project. 

If it is an npm package you can use `npm link`

if it an `obsidian plugin` then you can use symlink. 

plugins in obsidian needs to be in `.obsidian/plugin` folder. 

## usage

```
ln -s /path/to/original /path/to/link
```

ref: https://www.howtogeek.com/297721/how-to-create-and-use-symbolic-links-aka-symlinks-on-a-mac/