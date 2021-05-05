# Models cheatsheet

## JSON
```
details:{
	type:'json'
},
```

## isIn
```
location_type:{
	type: 'string',
	isIn: ['interstate', 'intrastate','international','sez']
},	
```

## allowNull
```
location_type:{
	type: 'string',
	allowNull:true,
},	
```


## required
```
user:{
	model:'user',
	required:true
},
```

## refer to a model
```
user:{
	model:'user',
	required:true
},
```

## backlink model reference
```
changes:{
	collection:'change',
	via:'transaction',
},
```

## Many to many reference
```
```

## Number format (float)
```
change:{
	type: 'number',
	columnType: 'float8'
},
```

## Date format  (timestamp)
```
date: {
	type: 'ref',
	columnType: 'timestamptz'
},
```

## defaultsTo
```
status:{
	type:'string',
	isIn:['processed_not_claimed','processed','not_filed','void','draft'],
	allowNull: true,
	defaultsTo:'not_filed', <----
},
```