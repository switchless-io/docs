# Steps and stages 
---
- Keywords:[[patterns]]
- author: #alex
---
The term steps and stages can be interchangibly used. We internally use the term steps when the overall process is a short one and typically gets completed in a single user session. The terminology stages are used to represent intermediate steps in a long running process that takes days/weeks or months to complete. 



### Eg - Steps in Mr Albert getting started process/form

![CleanShot 2020-08-28 at 15.25.10](/Users/alex/ec2code/switchless/docs/docs/files/steps_in_getting_started_mralbert.png)

[[CleanShot 2020-08-28 at 15.25.10]]

![[assets_images.png]]

### Eg - Stages in GSTR3b filing - Mr Albert

![CleanShot 2020-08-28 at 15.26.52](/Users/alex/ec2code/switchless/docs/docs/files/stages_in_gstr3b.png)

## Pattern
![CleanShot 2020-08-28 at 15.26.52](/Users/alex/ec2code/switchless/docs/docs/files/stages_pattern.png)

1. A state that is complete is marked with a green tick mark
2. An active stage is highlighed 
3. A future stage is disabled. 



Typically we split a process into stages for handling some sort of complexity. Do definitely you can expect each of these stages to be in seperate EJS files most of the time. The follow pattern is for writting steps without repeating yourself. 

```ejs
<%
	var current_stage = 'business_info'; // current stage of the process 
	// This function determines how should each stage of the process should be visualised (as active or complete or disabled) when the 	 process is at `current_stage`. 
	var stageStatus=function(stage){ 
    // this variable helps the code understand the actual sequence of stages in your process
		var stages=['personal_info','business_info','your_plan','verify_submit'];
		// var current_stage = filing.stage;
		var active_stage_pos = stages.indexOf(current_stage); 
		var stage_pos=stages.indexOf(stage);
		if(stage_pos==-1) // invalid case
			return 'disabled';
		else if(stage_pos<active_stage_pos)
			return 'completed';
		else if(stage_pos==active_stage_pos)
			return 'active';
		else if(stage_pos>active_stage_pos)
			return 'disabled';
	}
%>
<br>
<h1>Getting Started</h1>
<div class="ui steps">
	<div class="<%=stageStatus('personal_info')%> step">
		<i class="truck icon"></i>
		<div class="content">
			<div class="title">Personal Info</div>
			<div class="description">Your contact details</div>
		</div>
	</div>
	<div class="<%=stageStatus('business_info')%> step">
		<i class="payment icon"></i>
		<div class="content">
			<div class="title">Business Info</div>
			<div class="description">How your business is registered</div>
		</div>
	</div>
	<div class="<%=stageStatus('your_plan')%> step">
		<i class="info icon"></i>
		<div class="content">
			<div class="title">Your plan</div>
			<div class="description">Choose your plan</div>
		</div>
	</div>
	<div class="<%=stageStatus('verify_submit')%> step">
		<i class="info icon"></i>
		<div class="content">
			<div class="title">Submit</div>
			<div class="description">Verify and submit</div>
		</div>
	</div>
</div>
```

