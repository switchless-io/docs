# Filtering emails shot from staging environment  

Create a filter from the backend to not send mails to email IDs not matching these patterns.  

## Criteria: 
1. All test emails should follow a pattern. Examples:  
	1. {username}+company_co@gmail.com  
	2. @company.com  

## How do I create multiple accounts matching this pattern?
If you want to create multiple accounts using the same email, use the '+' operator the create different versions of the email. Examples:   
- username+va_company_co@gmail.com and username+client_company_co@gmail.com  
- username+va@company.co and username+client@company.co  


## Implementation
Modify this in `MailgunService.sendEmail()` function: 

```
if(process.env.NODE_ENV=='development' || process.env.NODE_ENV!='production'){
    data.to=`some_common_email@gmail.com`;
      //if there are any emails matching the pattern, add them
      var emails=options.to.split(',')
      emails.forEach(function(email){
        if(email.includes('@company.co') || email.includes('company_co@gmail.com'))
          data.to+=','+email

      })

    }
```

