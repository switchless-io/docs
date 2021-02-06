# mobile specific html
---
- author: #alex 
---


## Using 'mobile only'/ 'table computer only'
This approach does not optimize for html size. This approach optimizes developer simplicity. 


simply use 
`mobile only row` and `tablet computer only row` in your grids

When you need performance use a different approach. 

## Using media queries 
```html
<style type="text/css">

	@media (max-width: 768px) { 
		/*mobile specific*/
		.ui.basic.segment.section {
			padding-top: 40px;
			padding-bottom: 40px;
		}
		.ui.basic.masthead.segment {
			padding-top:0px;
			padding-bottom: 20px;
		}
	}
	@media (min-width:769px) {
		/*every other screen specific*/
		.ui.basic.segment.section {
			padding-top: 100px;
			padding-bottom: 100px;
		}
		.ui.basic.masthead.segment {
			padding-top:50px;
			padding-bottom: 20px;
		}
	}
</style>
```