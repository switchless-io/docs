# Checkbox in a form
---
Keywords: [[checkbox]],[[ui pattern]]
Author: [[Anzal]]

---

UI:
![[Pasted image 20201210134947.png]]

HTML:
```
<div class="ui checkbox">
	<input type="checkbox" name="is_subscription_for_training" 
		<%(_.get(sub,'details.flags.is_subscription_for_training')==true)?"checked='checked'":''
		%> >
			<label>Check this box if this subscription is only for training purposes</label>
</div>
```

Backend:

```
_.set(new_sub,'details.flags.is_subscription_for_training',(req.body.is_subscription_for_training=='on')?true:false)
```

