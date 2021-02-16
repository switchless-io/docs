# Prevent multiple form submissions by using loader on buttons
---
- Keywords:
- author: #alex
---
When an HTML form is getting submitted, there's a chance that the same request is sent multiple times on multiple clicks on submit button. Prevent this by disabling the button on the first valid form submission.  
![loader](/files/Pasted image 1.png)  
- If you are using semantic library for form validation, make sure the disable class is added only if the form is valid  


```
$('.ui.form').form({
    fields: {
    
        category: {
            identifier: 'category',
            rules: [
            {
                type   : 'empty',
                prompt : 'Please select a category'
            }
            ]
        },
    
    }
}).submit(function() {
    if( $('.ui.form').form('is valid')) {
        $('.button').addClass('disabled')
        $('.button').addClass('loading')
        
        //do any other action to be performed on successful form submission here
        fbq('trackCustom', 'task_created', {});
    }

    
})
```