# User card circular image

This element is build using `items`. 

## Element
#### on computer
![[Pasted image 20210212152251.png]]

#### on mobile
![[Pasted image 20210212152434.png]]
On mobile, the image takes up more space. the item is made `unstackable`. 
#### code 
```
<div class='ui segment'>
	<div class="ui unstackable items">
		<div class="ui item">
			<div class="ui tiny circular image">
				<a class="ui image" href="https://www.linkedin.com/in/ranjanik/" target='_blank'><img src="/images/ranjani.jpg"></a>
			</div>
			<div class="content">
				<a href="https://www.linkedin.com/in/ranjanik/" target='_blank' class="ui large header">Ranjani Krishnakumar</a>
				<div class="meta">
				   <i class="linkedin icon"></i><a href="https://www.linkedin.com/in/ranjanik/" target='_blank'>linkedin.com/in/ranjanik</a>
				</div>
				<div class="description">
					Founder and chief marketer, emdash consulting LLP
				</div>

			</div>
		</div> 
	</div>
</div>
```



## Eg: Usage as testimonials
![[Pasted image 20210212151325.png]]
```
<div class="ui basic segment section">
	<div class="ui container justified">
		<h1 class="ui center aligned header" style='margin-top: 0;margin-bottom: 30px;font-size: 2.4em;color:#00296b' >
			People *really* like Mr. Albert
		</h1>
		<div class='ui stackable grid '>
			<div class="row">
				<div class='ui eight wide column'>

					<div class='ui raised segment' style="padding: 20px">
						<div class="ui unstackable items">
						    <div class="ui item">
						        <div class="ui tiny circular image">
						            <a class="ui image" href="https://www.linkedin.com/in/ranjanik/" target='_blank'><img src="/images/ranjani.jpg"></a>
						        </div>
						        <div class="content">
						            <a href="https://www.linkedin.com/in/ranjanik/" target='_blank' class="ui large header">Ranjani Krishnakumar</a>
						            <div class="meta">
						               <i class="linkedin icon"></i><a href="https://www.linkedin.com/in/ranjanik/" target='_blank'>linkedin.com/in/ranjanik</a>
						            </div>
						            <div class="description">
						                Founder and chief marketer, emdash consulting LLP
						            </div>
						            
						        </div>
						    </div> 
						</div>
						<div style="font-size: 1.4em">
								
							<h2>I no longer worry about GST.</h2>
							<p>As a small business owner and freelancer, I have three GST numbers and multiple sources of revenue. Just handling GST compliance every month made me break into hives. That's until I met Mr. Albert.
							</p>

							<p>Today, the only GST activity I do is pay. The Mr. Albert team makes sure they gather all invoices, ensure accuracy, upload all info, even create a challan, and remind me at regular intervals to pay up. I've never missed a deadline ever since I started working with Mr. Albert. But that's not the best part.</p>

							<p>Even since they handle my GST matters, I've never had a single moment of worry. They're proactive, ahead of time, communicative and thoughtful. If you're looking for help with your GST, consider this my wholehearted endorsement.</p>
						</div>
					</div>
				</div>
				<div class='ui eight wide column'>

					<div class='ui raised segment' style="padding: 20px">
						<div class="ui unstackable items">
						    <div class="ui item">
						        <div class="ui tiny circular image">
						            <a class="ui image" href="https://www.linkedin.com/in/gautam-bt-3589ba77/" target='_blank'><img src="/images/gautam.jpeg"></a>
						        </div>
						        <div class="content">
						            <a href="https://www.linkedin.com/in/gautam-bt-3589ba77/" target='_blank' class="ui large header">Gautam BT</a>
						            <div class="meta">
						               <i class="linkedin icon"></i><a href="https://www.linkedin.com/in/gautam-bt-3589ba77/" target='_blank'>linkedin.com/in/gautam-bt-3589ba77</a>
						            </div>
						            <div class="description">
						                Founder at bytebeam.io
						            </div>
						            
						        </div>
						    </div> 
						</div>
						<div style="font-size: 1.4em">
								
							<!-- <h2>Mr Albert is the easiest GST service out there</h2> -->
							<p>Mr Albert is the easiest GST service out there</p>
						</div>
					</div>
					<div class='ui raised segment' style="padding: 20px">
						<div class="ui unstackable items">
						    <div class="ui item">
						        <div class="ui tiny circular image">
						            <a class="ui image" href="https://www.linkedin.com/in/jubyabraham/" target='_blank'><img src="/images/juby.jpeg"></a>
						        </div>
						        <div class="content">
						            <a href="https://www.linkedin.com/in/jubyabraham/" target='_blank' class="ui large header">Juby Abraham</a>
						            <div class="meta">
						               <i class="linkedin icon"></i><a href="https://www.linkedin.com/in/jubyabraham/" target='_blank'>linkedin.com/in/jubyabraham</a>
						            </div>
						            <div class="description">
						                Founder at colortheory.in
						            </div>
						            
						        </div>
						    </div> 
						</div>
						<div style="font-size: 1.4em">
								
							<!-- <h2>Mr Albert is the easiest GST service out there</h2> -->
							<p>I have been using Mr. Albert for my GST filing for the past 7 months and its absolutely hassle free. The representative gets in touch with you and reminds you to provide any invoices that you have and rest is taken care. The dash board is pretty amazing for you to track your filing progress and it’s all in one place and easy to understand.</p>

							<p>I recommend Mr. Albert to all those people who are busy and don’t have the time to sit with your accounting and filing as this can save you a lot of time and manual errors.</p>

						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

```

