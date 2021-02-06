# verify email
---
- author: #alex 
---
A web app needs to get the email id of the user verified. 

Recommended methods for verifing email
- [[verify email with OTP]]
- [[verify email with JWT token]]

## Advantages of each style
### OTP verification
Use OTP to verify email when you can store the OTP in your db object. This flow is also useful when you want a certain flow to be continuous. A link or JWT based flow is breaking in nature. The user starts of with a browser window and via the link in the email ends up in a new window. 

The disadvantage is that you have to store the OTP in you DB. Although you can work around this if you want to put effort. 

### JWT verification 
This is useful if you want users to click a link to verify email. This style is particularly useful during forgot password flow. During signup however this flow can be interrupting in nature - you end up in a different browser window. 