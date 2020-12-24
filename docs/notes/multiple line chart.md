# Multiple line chart
---
- author: [[Alex]]

---
## Example
![[Pasted image 20201224213852.png]]

## Part of the controller code that generates the data for the chart
```
getDispenses: function (callback) {
	var end_date = new Date().toISOString().substr(0,10);
	var start_date = new Date();
	start_date.setMonth(start_date.getMonth()-1)
	start_date=start_date.toISOString().substr(0,10);

	if(!req.query.end_date)
		req.query.end_date= end_date;
	if(!req.query.start_date)
		req.query.start_date = start_date;

	var query = `
		SELECT date_trunc('hour', CAST("time" AS timestamp)) AS "time", sum("volume") AS "sum",device
		FROM dispense 
		WHERE org=$1 
		AND CAST("time" AS date) BETWEEN CAST($2 AS date)
		   AND CAST($3 AS date)
		GROUP BY date_trunc('hour', CAST("time" AS timestamp)),device
		ORDER BY date_trunc('hour', CAST("time" AS timestamp)) ASC;
		`;
	sails
		.sendNativeQuery(query, [req.org.id,req.query.start_date,req.query.end_date])
		.exec(function (err, result) {
			callback(err, result.rows);
		});
},
getDispenseChart: ["getDispenses",function (results, callback) {
	var data = {
		labels: [],
		datasets: [],
	};
	var colors=[
		"rgba(255, 205, 86, 1)",
		"rgba(255, 99, 132, 1)",
		"rgba(55, 162, 235, 1)",
		"rgba(74, 192, 192, 1)",
		"rgba(153, 102, 255, 1)",
		"rgba(202, 203, 207, 1)",
		"rgba(255, 160, 65, 1)",
		"rgba(255, 160, 65, 1)",
	]
	results.getDispenses.forEach(function (dispense) {
		var dataset=null;
		data.datasets.forEach(function(ds){
			if(ds.label == 'device('+dispense.device+')')
				dataset=ds;
		})
		if(!dataset){
			dataset = {
				label: 'device('+dispense.device+')',
				data: [],
				fill: false,
				borderColor: colors[data.datasets.length%colors.length],
				lineTension: 0.1,
				pointRadius: 0,
				pointHitRadius: 5,
				spanGaps: false,
			};
			data.datasets.push(dataset);
		}
		dataset.data.push({
			x:dispense.time,
			y:dispense.sum,
		});
	});
	
	callback(null, data);
}],

```

## Front end
### html
```
<div class='ui segment'>
	<h3 style="margin-top: 0px;">Dispense log</h3>
	<canvas id="dispense_log" width="100" height="100"></canvas>
</div>
```
### Javascript 
```
var ctx = document.getElementById('dispense_log');
new Chart(ctx,{
    "type":"line",
    "data":<%-JSON.stringify(chart_data.dispense_log)%>,
   
    "options":{
            responsive: true,
            title: {
                display: false,
                text: 'Chart.js Line Chart'
            },
            legend:{
                display:false
            },
            tooltips: {
                mode: 'index',
                intersect: false,
            },
            hover: {
                mode: 'nearest',
                intersect: true
            },
            scales: {
                xAxes: [{
                    display: true,
                    // scaleLabel: {
                    //  display: false,
                    //  labelString: 'Month'
                    // }
                    type:'time',

                    time:{
                        // unit:'day'
                        minUnit: 'hour',
                        tooltipFormat:'MMM Do, h:mm a',
                        // displayFormats: {
                        //   day: 'MMM D',
                        //   week: 'MMM YYYY',
                        //   month: 'MMM YYYY',
                        //   quarter:   'MMM YYYY'
                        // }
                    },
                    distribution:'linear'
                }],
                // yAxes: [{
                //  display: true,
                //  scaleLabel: {
                //      display: true,
                //      labelString: 'Value'
                //  }
                // }]
            }
        }
});
```