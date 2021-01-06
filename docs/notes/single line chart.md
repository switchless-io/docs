# Single line chart
---
- author: #alex

---

## Example
![[Pasted image 20201224215235.png]]
## Controller code
this is the relevant controller code within an asyncauto.
```javacript
getDispenses: function (callback) {
	var query = `SELECT date_trunc('hour', CAST("time" AS timestamp)) AS "time", sum("volume") AS "sum"
FROM dispense 
WHERE org=$1 
GROUP BY date_trunc('hour', CAST("time" AS timestamp))
ORDER BY date_trunc('hour', CAST("time" AS timestamp)) ASC;
`;
	sails
		.sendNativeQuery(query, [req.org.id])
		.exec(function (err, result) {
			callback(err, result.rows);
		});
},
getDispenseChart: [
	"getDispenses",
	function (results, callback) {
		var data = {
			labels: [],
			datasets: [],
		};
		var dataset = {
			label: "Dispense volume",
			data: [],
			fill: false,
			borderColor: "rgb(75, 192, 192)",
			lineTension: 0.1,
			pointRadius: 0,
			pointHitRadius: 5,
			spanGaps: false,
		};
		results.getDispenses.forEach(function (dispense) {
			data.labels.push(dispense.time);
			dataset.data.push(dispense.sum);
		});
		data.datasets.push(dataset);
		callback(null, data);
	},
],

```

Front end code is similar to that of [[multiple line chart#Front end]]