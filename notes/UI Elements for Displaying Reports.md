# UI Elements for Displaying Reports

---

author: #anzal 

--


## Report example:
![[Pasted image 20210317102435.png]]


## Tool-tip (Popup)
On hover, a popup shows up:
![[Pasted image 20210317102624.png]]

Implementation:
CSS:
```CSS
/* Tooltip container */

.tooltip {

position: relative;

display: inline-block;

border-bottom: 1px dotted black; /* If you want dots under the hoverable text */

}

  

/* Tooltip text */

.tooltip .tooltiptext {

visibility: hidden;

width: 120px;

background-color: black;

color: #fff;

text-align: center;

padding: 5px 0;

border-radius: 6px;

  

/* Position the tooltip text - see examples below! */

position: absolute;

z-index: 1;

}

  

/* Show the tooltip text when you mouse over the tooltip container */

.tooltip:hover .tooltiptext {

visibility: visible;

}
```

HTML
```html
<a class="tooltip"></a>


<span class="tooltiptext">

</span>
```



## De-emphasized Text
Get text to appear like the denominator here:
![[Pasted image 20210317103001.png]]

Implementation:
```html
Normal Value
<span style="color:grey;font-size: smaller;">

De-emphasized text here

</span>
```


## Background color for cell
Notice the different background colors here:
![[Pasted image 20210317103211.png]]

Implementation:
```html

<%
bg_color='rgb(0,100,0,0.5);'
%>


<td style="background-color: <%= bg_color %>;">
```