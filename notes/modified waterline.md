# modified waterline/sails-hook-orm
---
- author: #alex 
- tags: #performance
---

## Use select and omit filters in populate

We are using modified waterline - https://github.com/alexjv89/waterline and modified version of https://github.com/alexjv89/sails-hook-orm

update your sails project with 
```
npm install https://github.com/alexjv89/sails-hook-orm#master --save
```

This makes it possible for you to do this - 
```
Invoice.find(filter)
	.populate('gstr3b',{select:['id','for']}) // this
	.populate('gstr1',{select:['id','for']}) // this
	.populate('gstr2a',{select:['id','for']}) // this
	.populate('gstr9',{select:['id','for']})
	.populate('documents')
	.sort('date DESC')
	.limit(limit)
	.skip(skip)
	.exec(callback);
```
## Gain
eg. gstr2a.details is extremely large json. This is a list invoices page. I am displaying 100 invoices in the same page. This results in massive return size from db. DB when running on t2.micro, this takes more than 60 secs and server times out. 

By selecting only relevant details for the page, the size of the db result reduces significantly and page loads in less than 1 sec. 

## Ref: 
https://github.com/balderdashy/waterline/pull/1613


https://github.com/balderdashy/waterline/pull/1613/files

https://github.com/balderdashy/waterline/pull/161

https://stackoverflow.com/questions/55617600/sailsjs-waterline-populate-records-with-select

