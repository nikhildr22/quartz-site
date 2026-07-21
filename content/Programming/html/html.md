# html dcuments
it strated with research docs, now its extensively used for evrything
started as text based, now its media rich
- its a markup language
- markup is not displayed, renderderd content is displayed

HTML use HTTP
![[Pasted image 20210401023857.png]]
## doctype
it indicated the standards / version of the document

notice that it starts with `<!` --> this somewhat like a metadata or you can also compare it to a comment that browser can understand
## html tag
root element of document
## head element
![[Pasted image 20210401024035.png]]
title 
meta
link
## body
content to be displayed

## demo
validator.w3,org
to check if the document is right

## head
![[Pasted image 20210401030250.png]]
### title
goes to the tab
### meta
for browers and search engines
### script
if u add script here, it'll run first no matter what
### style
### link
linking stylesheets
### base

### comments
```html
<!-- 
this is comment
-->
```

## Body
![[Pasted image 20210401030924.png]]
### text
#### headings
6 levels
![[Pasted image 20210401031358.png]]

#### blocks and inline
![[Pasted image 20210401031437.png]]
![[Pasted image 20210401031446.png]]
![[Pasted image 20210401031500.png]]

#### break and white spaces
![[Pasted image 20210401031937.png]]
br --> next line
`&nbsp` non breaking space --> just a space
``<hr />`` horizontal line
`&xx;` --> special symbols
#### displaying reference text
![[Pasted image 20210401032303.png]]
#### semantics
![[Pasted image 20210401032615.png]]
![[Pasted image 20210401032622.png]]
![[Pasted image 20210401032703.png]]
these are symantically relevent:
article tag appears only once in a doc.

header tag
footer tag
section tag


### Lists
3 type of list
![[Pasted image 20210401033533.png]]
```html
<ul>
	<li></li>
	<li></li>
	<li></li>
</ul>
	
<ol>
	<li></li>
	<li></li>
	<li></li>
</ol>

<!-- the order is here just for display -->

<dl>
	<dt></dt>
	<dd></dd>
<dl>
	
```
![[Pasted image 20210401033946.png]]
![[Pasted image 20210401033957.png]]
#### uses of lists
![[Pasted image 20210401034052.png]]
list with defined class can make magic happen

### Links

Linking documents
#### anchors
a tag
href attribute --> hypertext referance

![[Pasted image 20210401034504.png]]
href
- absolute
- relative

![[Pasted image 20210401034603.png]]

#### linking docs and linking within document
![[Pasted image 20210401034919.png]]
![[Pasted image 20210401034927.png]]
just like obsidian #aha 

#### Expanding link metadata
![[Pasted image 20210401035234.png]]
target attribute --> new tab
![[Pasted image 20210401041242.png]]
rel attribute is used for security measures
### Tables
![[Pasted image 20210401041446.png]]
remember that they are just for data and dont use it everywhere lol
#### defining tables
![[Pasted image 20210401041601.png]]
![[Pasted image 20210401041629.png]]
#### working with them
rowspan and colspan
#### formatting
![[Pasted image 20210401042146.png]]
border attribute can also be used
but we use css
![[Pasted image 20210401042257.png]]
for aliggning
![[Pasted image 20210401042348.png]]

### images
#### adding images
![[Pasted image 20210401045840.png]]

#### muliple sources
![[Pasted image 20210401050209.png]]
sorcet
sizes
based on screen size we use different images and different viewport width.

#### using images
picture tag
![[Pasted image 20210401050524.png]]
![[Pasted image 20210401050625.png]]
media query
![[Pasted image 20210401050723.png]]
![[Pasted image 20210401050902.png]]

# Planning for Accessibility
![[Pasted image 20210401051119.png]]
![[Pasted image 20210401051202.png]]
![[Pasted image 20210401051218.png]]
aria - standardizing for screenreaders and similar technologies
![[Pasted image 20210401051254.png]]

whats next:
![[Pasted image 20210401051419.png]]

[[HTML forms]]