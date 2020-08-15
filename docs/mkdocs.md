# Mk Docs

This is what we use to documenting things. 

## Requirements of a documentation system 
- tooling should be familiar
- documentation should be done by the creator - in this case the developer
- tooling should be efficient for creator - ie should be developer friendly 
- A tooling that fits developers helps do multiple iterations of the same document. 

## What we tried before
We tried wordpress. The problem with wordpress is that, specifically for a developer, there is a lot of overhead. 
You will have to head over to a website, enter username password and then then write content. 
By the time you head over the browser, login, half of your enthusiasm for writing is gone. 
Also you are bothered by whether you should create a post or a page.

Lets look at the workflow in Mkdocs. 
You are writing code and you come across an interesting idea. You command tab to the right sublime window. Create a file and start writing. 
Once you are done, you can choose you organise it. you can choose to commit it if you like it. you can choose to let it be there for a while if you are not satisfied with it. 

The obvious disadvantage for a system like this is that it is only suited for developer writters. Its going to be super difficult for a non developer to contribute. 

## Our flavor of mkdocs 
[Swithless flavor of mkdocs](https://github.com/switchless-io/mkdocs)

## Setup 

The generator for switchless is available in switchless-cli. Run the switchless cli to install mkdocs with our flavor.

`./node_modules/@switchless-io/cli/index.js` 

choose `install`, choose `mkdocs` from the menu.

If you are starting a new project, mkdocs in included in the `web-app` template.

### Integrate with read the docs 
- advanced settings
	- defaut version - latest
	- default branch - master
	- single version - tick this checkbox 
- domains 
	- add your domain 
		- canonical - tick this checkbox
		- always use http - tick this checkbox 

## Usage 
- Write doc
- Organise it under folders etc
- Update the Navbar if required
- Commmit to repo

## Ref: 
- [https://www.mkdocs.org/user-guide/deploying-your-docs/](https://www.mkdocs.org/user-guide/deploying-your-docs/)