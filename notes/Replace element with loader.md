---
author: #anzal 
---

# Replace element with loader
On checking a box:

![[Pasted image 20210406211248.png]]

The box gets replaced by loader:

![[Pasted image 20210406211328.png]]


## Implementation

HTML:

```html
<div class="ui toggle checkbox" data-id="<%=org.id%>">

	<input type="checkbox" name="tg_non_tg" data-id="<%=org.id%>" 

	<label>

	<%if(_.get(org,'details.tg_non_tg')){%>

	<%=_.get(org,'details.tg_non_tg')%>

	<%}else{%>

	<span style='color:grey'><i>not set</i></span>



	</label>

  

</div>

<div class="ui active inline mini loader" style="display: none;" ></div>
```

JS:
```javascript
$('.ui.checkbox').checkbox({

// check all children

onChecked: function() {

	var this_checkbox=$(this)

	this_checkbox.parent().parent().find('.loader').show()

	this_checkbox.parent().hide()

	var org_id=$(this).attr('data-id')

  
  

	$.post("/api/org/edit", {body:body},function(result,status){


		if(status=='success'){


		this_checkbox.parent().parent().find('.loader').hide()

		this_checkbox.parent().show()

		}

	});

  


},

// uncheck all children

onUnchecked: function() {

var this_checkbox=$(this)

this_checkbox.parent().parent().find('.loader').show()

this_checkbox.parent().hide()

var org_id=$(this).attr('data-id')

  
  

$.post("/api/org/edit", {body:body}, function(result,status){



if(status=='success'){


this_checkbox.parent().parent().find('.loader').hide()

this_checkbox.parent().show()

}

});

}

})

```