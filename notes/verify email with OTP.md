# Verify email with OTP
---
- author: #alex 
---


### email template
```javascript
<% include css_for_email %>
<div class='ui container'>
	<div class='ui segment'>
		<p>Hi <%=lead.name%>,</p>

		<p>Please verify your email address.</p>
		<p>Your OTP for verifying your email address:</p>
		<h3><%=lead.email_otp%></h3>
		<p>Please enter above OTP in your getting started form.</p>
		<p>You are receiving this email because you filled in your details on https://www.mralbert.in/getting_started. If you did not do this, please report to us at support@mralbertgst.freshdesk.com</p>

			
	</div>
</div>
```

### Trigger email
```javascript
var data={
	title:'Send Email - Verify email',
	options:{
		template:'email_otp',
		lead:lead.id,
	},
};
await queue.add('send_transactional_email',data);
```

### Verify OTP
```javascript
if(lead.email_otp==req.body.email_otp.trim())
	update_lead.is_email_valid=true;
Lead.updateOne({id:lead.id},update_lead).exec(function(err,result){
	res.redirect(`/getting_started/${lead.id}/business_info`);
});
```