# Mobile friendly filter using accordian

## Example
![[CleanShot 2021-03-19 at 10.05.55.gif]]
### When filter is minimised
![[Pasted image 20201224165216.png]]
### When filter is opened to edit
![[Pasted image 20201224165155.png]]

### When filter is applied and is minimised
![[Pasted image 20201224165344.png]]

### When filter is applied and is opened to edit
![[Pasted image 20201224165410.png]]

### to start with folded filter
remove the class `active` from `content` and `title`

### Code

```

<div class='ui container'>
	<div class="ui vertical large accordion fluid menu">
		<div class="item">
			<a class="active title">
				<i class="dropdown icon"></i>
				Filter 
				<%if(req.query.sites || req.query.devices){%>
					<div class="ui teal horizontal label">Applied</div>
				<%}%>
			</a>
			<div class="active content">
				<form class="ui form" action='' method="GET">
					<div class="field">
						<label>Sites:</label>
						<div class="ui fluid multiple search selection dropdown tags">
							<input type="hidden" name="sites" value='<%=req.query.sites?req.query.sites:''%>'>
							<i class="dropdown icon"></i>
							<div class="default text">Sites</div>
							<div class="menu">
								<%sites.forEach(function(s){%>
									<div class="item" data-value='<%= s.id %>'><%= s.name %></div>
								<%})%>
							</div>
						  </div>
					</div>
					<div class="field">
						<label>Devices:</label>
						<div class="ui fluid multiple search selection dropdown tags">
							<input type="hidden" name="devices" value='<%=req.query.devices?req.query.devices:''%>'>
							<i class="dropdown icon"></i>
							<div class="default text">Devices</div>
							<div class="menu">
								<%devices.forEach(function(d){%>
									<div class="item" data-value='<%= d.id %>'><%= d.name %></div>
								<%})%>
							</div>
						  </div>
					</div>
					
					<div class="two fields">
						<div class="field">
							<label>Start date</label>
							<div class="ui calendar" id="rangestart">
								<div class="ui input left icon">
									<i class="calendar icon"></i>
									<input type="text" name="start_date" placeholder="Start" value="<%=req.query.start_date%>">
								</div>
							</div>
						</div>
						<div class="field">
							<label>End date</label>
							<div class="ui calendar" id="rangeend">
								<div class="ui input left icon">
									<i class="calendar icon"></i>
									<input type="text" name="end_date" placeholder="End" value="<%=req.query.end_date%>">
								</div>
							</div>
						</div>
					</div>
					
					<div class="ui buttons">
						<div class='ui orange left aligned button' id='submit_form'>Apply filter</div>
						<div class='ui blue right aligned button' id='reset_form'>Reset</div>
					</div>
				</form>
			</div>
		</div>
	</div>
</div>

<script type="text/javascript">
	$(document).ready(function(){
		$('.ui.accordion').accordion();
		$('.dropdown.tags').dropdown();
		$('#submit_form').click(function(){
			console.log('clicked on form submit');
			$("form").submit();
		});
		$('#reset_form').click(function(){
			window.location = window.location.pathname;
			$(this).addClass('loading');
		});
		$('#rangestart').calendar({
			type: 'date',
			endCalendar: $('#rangeend'),
			formatter: {
				date: function (date, settings) {
					if (!date) return '';
					var day = date.getDate();
					var month = date.getMonth() + 1;
					var year = date.getFullYear();
					return year + '/' + month + '/' + day;
				}
			}
		});
		$('#rangeend').calendar({
			type: 'date',
			startCalendar: $('#rangestart'),
			formatter: {
				date: function (date, settings) {
					if (!date) return '';
					var day = date.getDate();
					var month = date.getMonth() + 1;
					var year = date.getFullYear();
					return year + '/' + month + '/' + day;
				}
			}
		});
	})
</script>
```