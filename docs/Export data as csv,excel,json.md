# Export data as csv/xls/json
keywords: [[patterns]]

use this ui pattern - [[Right floated icon download dropdown]]


## Export as xls
Do this in sequence: 
- [[Write excel file]]
- [[Download file]]

```
if(req.query.download_as=='xls' || req.query.download_as=='csv'){
	var ws = XLSX.utils.json_to_sheet(sheet_data);
	var wb = XLSX.utils.book_new();
	XLSX.utils.book_append_sheet(wb, ws, 'invoices');

	var time = new Date().getTime();
	var out = XLSX.writeFile(wb, 'out_'+req.user.id+'_'+time+'.'+req.query.download_as);
	res.attachment('invoices.'+req.query.download_as);
	var downloading = await sails.startDownload('out_'+req.user.id+'_'+time+'.'+req.query.download_as);
	downloading.pipe(res);
}
```



## Export as csv
Same as xls. When exporting the file using xlsx, set the file extension as `csv`. 

## Export as json
using fs, write file to server. Then download the file. 
```
fs.writeFileSync('out_'+req.user.id+'_'+time+'.json', JSON.stringify(sheet_data,null,'\t'));
res.attachment('invoices.json');
var downloading = await sails.startDownload('out_'+req.user.id+'_'+time+'.json');
downloading.pipe(res);
```