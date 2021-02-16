# Breadcrumbs

## Breadcrumbs used in Mr Albert
![[Pasted image 20210126142157.png]]
```ejs
<div class="ui breadcrumb">
	<a class="section" href='/gstin/<%=req.gstin.value%>' ><%=req.gstin.business_name%></a>
	<i class="right angle icon divider"></i>
	<a class="section" href='/gstin/<%=req.gstin.value%>/filings?type=gstr1'>Filing</a>
	<i class="right angle icon divider"></i>
	<div class="section">GSTR 1: <%=filing.for%></div>
</div>
```

