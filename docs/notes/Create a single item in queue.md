# Create a single item in queue
---
- author: #alex 
---

```javascript
var data={
	title:'Send Email - We are preparing your GSTR3B',
	options:{
		template:'getting_ready_to_file_gstr3b',
		gstin:req.gstin.id,
		filing:req.params.filing_id,
	},
	info:{}
};
// assuming this is called inside an async function
await queue.add('send_transactional_email',data);
```