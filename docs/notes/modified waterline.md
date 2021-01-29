# modified waterline/sails-hook-orm
---
- author: #alex 
- tags: #performance
---

We are using modified waterline - https://github.com/alexjv89/waterline and modified version of https://github.com/alexjv89/sails-hook-orm

update your sails project with 
```
npm install https://github.com/alexjv89/sails-hook-orm#master --save
```

This makes it possible for you to do this - 
```
console.log('\n\n\n-------- 7');
Invoice.find(filter)
	.populate('gstr3b',{select:['id','for']})
	.populate('gstr1',{select:['id','for']}) // this
	.populate('gstr2a',{select:['id','for']})
	.populate('gstr9',{select:['id','for']})
	.populate('documents')
	.sort('date DESC')
	.limit(limit)
	.skip(skip)
	.exec(callback);
```

## Ref: 
https://github.com/balderdashy/waterline/pull/1613


https://github.com/balderdashy/waterline/pull/1613/files

https://github.com/balderdashy/waterline/pull/161

https://stackoverflow.com/questions/55617600/sailsjs-waterline-populate-records-with-select

