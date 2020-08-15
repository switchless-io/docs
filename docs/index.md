# Welcome to Switchless
A choice of tech stack selected for a single person company

This is an opinionated stack. 

We made a bunch of choices regarding various parts of a web stack. Of couse there are 1000s of way to build a web stack. This is just one way, but this is one way that we found ourselves reusing again and again. The idea with switchless is to give you a set of default choices for web stack so that you dont get lost in analysis paralysis. This choice of tech stack will free up your brain space to help you focus on your business/operational requirements instead spending time deciding tech stack. 

Someday you will overgrow these default choices. You can come back and thank us then. 

## Who is this tech stack for?
This tech stack is designed for a `company of one`. If you are building a product company all by yourself, you dont have a lot of time to waste. You are writing code, talking to customer, handling operations, managing consultants. This tech stack is specifically designed for the constaints of a single person team. 

Of course, if your team is more than one person, you can still use this stack but the usabilty of the stack becomes a grey scale. At the other end of the grey scale, if you have a 100 person engineering team, you will most likely outgrow this stack or will customise it heavily. 

## Constraints of single person team
This tech stack respects the following constraints of a single person company:

- minimise switching cost
	- master one programing language
	- avoid frontend/backend complexities.. keep it simple.. keep it server rendered most of the time.
- avoid managing servers as much as possible - embrase managed services
- focus on things in this order
	- customer 
	- product 
	- reliabilty 
	- avoid fancy (fancy ui/fancy workflow - they are likely to be flaky)
	- minimise complexity
	- lesser the better

## Features / abilities 
- Ability to send and receive emails 
- Ability to pipe, process and visualise logs 
- Ability to login
- Ability to collect payments

## Stack choice
- Bull 
- Mailgun
- Passportjs
- Zoho invoice