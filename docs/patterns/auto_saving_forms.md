# Auto Saving Forms

To auto save forms,  
- When user starts creating an object through a form, create a draft entry of the the form in database  
    - Redirect the user to the edit page of this draft object  
- On user editing the page, trigger an ajax call to save the form in DB  
    - There are couple of triggers to save the form  
        - Periodically - example, every 10 seconds  
        - On event - example, when the user moves to the next field  

```

//Save on form change
  $('.form').change(function(){
      save()
 })

//Save every 10s
 // setInterval(save,10000);


// trigger a save every 10s
var save = function autosave() {
    jQuery('form').each(function () {
        jQuery.ajax({
            url: "/form/:form_id/save", //url to save the form
            data: jQuery(this).serialize(),
            type: 'POST',
            success: function (data) {
                console.log('saved:');
            }
        });
    });
}


```