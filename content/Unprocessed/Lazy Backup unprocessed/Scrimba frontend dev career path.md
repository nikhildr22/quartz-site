  html - ==hypertext markup language==


`img` tag is self closing tag.
`src` attribute spefifies the image source.
`width` attr size of the image.

100% width will make the image responsive to size of the screeen.

html tags can be nested.
we indent them for readability.


`button` tag creates a button.

anchor  tag `a`  uses href attribute to add the link.

`target=_balnk_` will open the link in new tab.


---
# Document structure in html

it mainly has a head and body.

body contains content
head contains metadata.

`<!doctype html>` html tag to specify the document is a html document.




---
# HTML lists

2 types:
1. ordered list
2. unordered list

```html
<ol>
	<li>item</li>
	<li>item</li><li>item</li>
	<li>item</li>

</ol>


<ul>
	<li>item</li>
	<li>item</li><li>item</li>
	<li>item</li>

</ul>
```

---
# css
![[Pasted image 20221128085828.png]]

# comment in css
similar to multiline comment in c and c#
```css
/* red, blue, yellow, etc */
/* This is comment in css*/
```

# display: inline; vs block
force the element to display inline event if its display block.
![[Pasted image 20221128090426.png]]

![[Pasted image 20221128090452.png]]

# add white space around the element.
we should use margin to add white space around the element.

# gather elements inside single block.
`<div>` can be used  to gather elements inside single block.


class selector starts with  `.`

# Margins:
```css
margin-top
margin-botton
margin-right
margin-left

```

>Sometimes margins of adjacent elements collapse into each other and Larger margin will take prominence.

>==Add a Border to all element you want to size or style so that you can easiily distinguish between margins and border and paddoing and also contrasts==
# Horizontally centering element in CSS

#important 
## 3 things to consider when centering an element:
1.  **Display Block** - because we should be able to control the entire horizontal space and display block helps us achieve that.
2. element must have a **width** - because, you cant center an element if it covers up entire screen
3. **margin-left/right="auto"**

```css
img {

	display: block;
	width: 200px;
	margin-left: auto;
	margin-right: auto;

}
```




---
# padding


while margin adds space outside the element.
Padding will add space inside the element - between content and border of element .

>==Note that `auto` is invalid value for  padding, padding should always be a definite value (unlike margin)==




---
# border

```css
border: 8px solid blue;

border-radius: 100px;
```
![[Pasted image 20221128092402.png]]
# The box model
- Margin
- Border
- Padding
- Content


# Using good contrasts for background
Bad contrasts will have bad User experience for visually impaired users and also normal users.
use contrast checker to find out the best contrast for the elements with respect to their background.

![[Pasted image 20221128093627.png]]

![[Pasted image 20221128093810.png]]

https://userway.org/contrast/?fg=ecff00&bg=ffffff




---
# flexbox

```css
.nav-wrapper {

	display: flex;
	justify-content: center;

}
```

![[Pasted image 20221128094409.png]]

we must wrap all elements  we want to arrange inside a flex container(div)
and then use `display:flex` to use flexbox features.

```css
/* Positional alignment */
justify-content: center;     /* Pack items around the center */
justify-content: start;      /* Pack items from the start */
justify-content: end;        /* Pack items from the end */
justify-content: flex-start; /* Pack flex items from the start */
justify-content: flex-end;   /* Pack flex items from the end */
justify-content: left;       /* Pack items from the left */
justify-content: right;      /* Pack items from the right */

/* Baseline alignment */
/* justify-content does not take baseline values */

/* Normal alignment */
justify-content: normal;

/* Distributed alignment */
justify-content: space-between; /* Distribute items evenly
                                   The first item is flush with the start,
                                   the last is flush with the end */
justify-content: space-around;  /* Distribute items evenly
                                   Items have a half-size space
                                   on either end */
justify-content: space-evenly;  /* Distribute items evenly
                                   Items have equal space around them */
justify-content: stretch;       /* Distribute items evenly
                                   Stretch 'auto'-sized items to fit
                                   the container */

```

---
# business card project

![[Pasted image 20221128095211.png]]

![[Pasted image 20221128095307.png]]

![[Pasted image 20221128095430.png]]
a good alt text on the image will make you standout as a developer.
it also help with search engine indexing.

>==All elements inside a flexbox are converted into individual columns==


# utility class
![[Pasted image 20221128100133.png]]
![[Pasted image 20221128100215.png]]
![[Pasted image 20221128100228.png]]

here, the border-blue is the utility class that is being reused.


---
# CSS inheritence

*Examples of inheritence ?*
>we can use text-align property to align all elements  inside the body to center/right/left = TRICK


![[Pasted image 20221128100557.png]]
DRYer - Dont repeat yourself.

lesss code = smaller surface area for bugs

less bugs = effiecient developer 

[[inherited props in css]]

*Some examples of not inherited props:*
> Note that fonts dont inherit.
> So, we either have to declare the font or we can make it inherit from the parent. `font-family: inherit;`


---
# Fonts

## Web-safe fonts
https://www.w3schools.com/cssref/css_websafe_fonts.php

these are the fonts that are already present in the browser.
### Best Web Safe Fonts for HTML and CSS

The following fonts are the best web safe fonts for HTML and CSS:

-   Arial (sans-serif)
-   Verdana (sans-serif)
-   Tahoma (sans-serif)
-   Trebuchet MS (sans-serif)
-   Times New Roman (serif)
-   Georgia (serif)
-   Garamond (serif)
-   Courier New (monospace)
-   Brush Script MT (cursive)


```css
font-family: Verdana, Geneva, Tahoma, sans-serif;
```

difference between serif and sans serif:
![[Pasted image 20221128102041.png]]

# shorthand properties

![[Pasted image 20221128102132.png]]
![[Pasted image 20221128102144.png]]

*How do you remember the order?*
use the **clock** to remember the order: top, right, bottom ,left
![[Pasted image 20221128102235.png]]



![[Pasted image 20221128102350.png]]

---
# Space exploration site

use https://unsplash.com/ to find good background images.
```css
body {

background-image: url("images/universe.jpg");

}
```

`url()` is a CSS function.



---
# Google fonts
instead of going to actual google fonts site, you can simply google , because the search works better from google than google-fonts site.

![[Pasted image 20221129094017.png]]
![[Pasted image 20221129094050.png]]
copy the header elements.
copy the css property.

> Note that fonts dont inherit.
> So, we either have to declare the font or we can make it inherit from the parent. `font-family: inherit;`

```css
.btn {

padding: 6px 12px;

background: white;

border: none;

font-family: inherit;
}
```

For fonts that are not in cdn.
we can download the font from any place.
they'll have `.ttf` extension.

we need to use [[At-rules]] to define the font. then we can use inside css properties just like any other font.
![[Pasted image 20221129094632.png]]

```css
@font-face {

src: url("Corleone.ttf");

font-family: Corleone;

}

  

h1 {

font-family: Corleone;

}
```

>we can name the font whatever we want.



---
# Span Tag

spans are **inline** elements.
we can use span to **format individual elements**.

```css
  

.underline {

border-bottom: 4px solid white;

}
```
we can use border as well to underline items.
also `text-decoration` can be used.


# css selector : ID

id can be used only once.
if we use id multiple times, it'll be invalid html.


# animated background

we can use animations with format gif, webp etc

`.webp` has better compression and will be of less size when compared to `.gif`

you can goto https://giphy.com/ to get whatever animated image you want.

then we can use css url() function to use the gif/webp
```css
background-image: url("https://media.giphy.com/media/S0n9aBFbzqdTrb5Gm8/giphy.gif");
```

---

Hero section - section on the top of the body of every site which emphasized the main theme of the site.

Text-Shadow:
![[Pasted image 20221129104852.png]]
we can also have blur:
![[Pasted image 20221129104925.png]]

Sometimes we just need to add a shadow to enhance the visibility.
![[Pasted image 20221129110600.png]]

# Making image round:
make **border-radius : 50%**
# select multiple elements in css
we can use comma to select multiple elements
```css
h1, h2, h3, h4, {

text-shadow: 0px 0px 1px black;

}
```


---
# Align items in flexbox

```css
justify-content:

start, center, end, space-around,

space-evenly, space-between

align-items:

start, center, end
```

by default, the flex direction will be row.
Thus, we can use justify-content to arrange the elements in a row.

and you can use align-items to control the vertical(column) positioning.

# flex direction

it can be row(default) or column.
it determines the main axis(if its a row/column)

Note:
```css
display: flex;

flex-direction: column;

justify-content: start;

align-items: center;
```

make sure first you add justify-content  and then align-items for better clarity and avoid confusion.

# :hover pseudo class

we can add any effect when user hovers over the elemet


# Gradients
we'll use css fucntions to get a gradient background
```css
background: linear-gradient(#a2d2ff, #EFB0C9);
```
this'll add gradient from top to bottom.




---
---
# Making websites interactive - js

script tag  inside the body.

for good practice, create index.js file, and add a reference to it in index.html file.
```html
<script src="index.js"></script>
```


`let` keyword can be used to declare a variable.

`console.log()` can be used to debug.

`onclick="myFunc()"` can be used to add function to the button click event.


when the variable is out of scope, we'll get this error `ReferenceError: totalTime is not defined`

DOM resides in global scope.

```js
document.getElementById("count").innerText = 5
```
we can use this to get text of an element.

>we use camelCase in js naming


# Type casting
```js
parseInt()
parseFloat()
```
we can use these to convert text to int/float

# DOM
document object model
![[Pasted image 20221201052118.png]]
![[Pasted image 20221201052143.png]]

# string concatenation
we can use `+` to concatenation pf strings.

Note:
>concatenating string with int will result in string concatenation

we can use `+=` shorthand for increment.

Checkout the difference between `innerText` and `textContent`



# strictly equals vs equals
```js
//=== vs ==
```
use === preferrably because, its a strict comparison and we can avoid a lot of errors that arise due to type casting.

## Linking CSS
```html
<link rel="stylesheet" href="index.css">
```

`rel` attribute is used to define the **relation** between the linked file and the html file.
`src` attribute  is used to define the source address of the linked file.

## Arrays in Js
- they are zero indexed.
- `[]` they are inside square bracket.
- `myArray.length` can be used to get the size of the array.
- Js arrays allow multiple data types(complex/composite datatypes)
- `myArray.push(item)` is used to push an item into the array.
- `myArray.pop()` will remove the last item of the array.
- `myArray.shift()` removes the first element
- `myArray.unShift()` will add the item in first position.


## for loop in js


```js
// START FINISH STEP SIZE

for ( let count = 1; count < 11; count += 1 ) {

console.log(count)

  

}
```
## Random numbers
`Math.random()` we can use `Math` library to get random number.
it return numbers from ==0.000 to 0.999==

since the range is between 0 and 1, we need to multiply by 1-10 get the random numbers of that range.

we need to use `Math.floor()` to round down the number ==it basically removes the decimals==.

but the resulting range will be starting from 0.
thus we need to add `1` if we want to start it from 1. `2` if we want to it to start from 2.

```js
let randomNumber = Math.floor( Math.random() * 6 ) + 1
//This returns random number in the range 1,6
```

>since there is a floor `Math.random()` will never be 1.
>Thus the range will be maximun the last number with what we multiplied with.


## Logical Operators
```js
/*
&& --> AND
|| --> OR
*/
```

## Js Objects
```js
let player = {

		name: "Per",
		
		chips: 145

}
```

In Js, the objects are dynamic. you dont need a class to create an object.

==we can use `.` dot notation and also `["key"]` brackets notation to access the members of the object.==

### we can also have a funtion inside the objects
```js
let player = {

	name: "Per",
	
	chips: 200,
	
	sayHello: function() {
	
		console.log("Heisann!")
	
	}

}
```


# box-sizing css property 
```css
input {

	width: 100%;
	
	padding-left: 10px;
	
	padding-right: 10px;
	
	box-sizing: border-box;

}
```

in the above example, if there is no box-sizing , the width of the input box will be **100% width + 20px padding,** so this'll go out of the screen.
Thus, we need to use `box-sizing: border-box;` to make the box sizing does not go out of the border.

# addEventListener
```js
inputBtn.addEventListener("click", function() {

console.log("Button clicked from addEventListener")

})
```
we can add event listener dynamically using Js.

# const vs let
```js
let myLeads = []

const inputEl = document.getElementById("input-el")

const inputBtn = document.getElementById("input-btn")
```
we should use `const` for those variables that never will be reassigned later. 
In Js, we can make dom elements const as we'll not be reassignining them later

# innerHTML
```js
let myLeads = ["www.awesomelead.com", "www.epiclead.com", "www.greatlead.com"]

const inputEl = document.getElementById("input-el")

const inputBtn = document.getElementById("input-btn")

const ulEl = document.getElementById("ul-el")

  

inputBtn.addEventListener("click", function() {

myLeads.push(inputEl.value)

console.log(myLeads)

})

  
  

for (let i = 0; i < myLeads.length; i++) {

ulEl.innerHTML += "<li>" + myLeads[i] + "</li>"

}
```

we should use `innerHTML` instead of `textContent` when we want to render HTML instead of text.

It is more like Declarative way of programming, rather than imperative way of programming.
[[ReactJs#WHy react? Its declarative.]]

>==Note that DOM manipulation is expensive,== so always try to minimize the number of times the DOM manipulation happens by optiming your code.
>In the above example, instead of doing DOM manipulation inside for loop, we can do dom manipulation at the end once we have all data we need.

```js
// 1. Create a variable, listItems, to hold all the HTML for the list items

// Assign it to an empty string to begin with

let listItems = ""

for (let i = 0; i < myLeads.length; i++) {

// 2. Add the item to the listItems variable instead of the ulEl.innerHTML

listItems += "<li>" + myLeads[i] + "</li>"

}

// 3. Render the listItems inside the unordered list using ulEl.innerHTML

ulEl.innerHTML = listItems
```
# createElement and append
this is more of imperative  way of programming

```js
for (let i = 0; i < myLeads.length; i++) {

// ulEl.innerHTML += "<li>" + myLeads[i] + "</li>"

// create element

// set text content

// append to ul

const li = document.createElement("li")

li.textContent = myLeads[i]

ulEl.append(li)

}
```

# anchor tags
```html
<a target='_blank'
```
this'll open link in new tab.


# Template strings/template literals

```js
function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
     // listItems += "<li><a target='_blank' href='" + myLeads[i] + "'>" + myLeads[i] + "</a></li>"
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

we can use template string to format strings.
using template strings, we can write declarative  code in more human readable format, so that the debugging will be easy. and also less number of bugs due to readability .

# HTML lists

```css
list-style: none; 
/*This'll remove all the list styling from list(remove bullets/numbers ) */
```

# chrome extension 
![[Pasted image 20221206041429.png]]

## manifest.json
json is used to store and transfer data.
in json files, the keys are enclosed by double quotes, unlike Js Objects where the keys were not enclosed by double quotes.

```json
{
    "manifest_version": 3,
    "version": "1.0",
    "name": "Leads tracker",
    "action": {
        "default_popup": "index.html",
        "default_icon": "icon.png"
    }
}
```

`"manifest_version"` --> which version of json file
`"action"` --> default action whenn the icon is clicked


we need to add `min-width` to the body of our popup to set the width of popup
```css
body {
    margin: 0;
    padding: 10px;
    font-family: Arial, Helvetica, sans-serif;
    min-width: 400px;
}
```

`"version"` --> version of chrome extension


>Goto Chrome extension and use load extension option to install extension on your local browser 


# localStorage
in developer tools, we got the Application window:
![[Pasted image 20221206042135.png]]

here we can see Local storage.
![[Pasted image 20221206042205.png]]

This data is local and unique to me.
![[Pasted image 20221206042240.png]]

`localStorage.setItem()` --> the data added with this method will persist even after refresh.
syntax for using localStorage :

```js
// localStorage.setItem(key, value)
// localStorage.getItem(key)
// localStorage.clear()  --> Thid'll clear all localStorage items
// PS: both key and value need to be strings
```
==both key and value need to be strings==
Thus we need to use `JSON.stringify(item)` and `JSON.parse(item)` to convert to string and convert back
Thus, if we need to store any object or array, we need to stringify to store in local storage.


# Truthy and falsy values
in Js,a valid value is a truthy value, it does not necessarily be a boolean.

How to remember the falsy values?
==Important==
```js
// false
// 0
// ""
// null -> how you as a developer signalize emptiness
// undefined -> how JavaScript signalizes emptiness
// NaN
```

real world xample:
```js
let currentViewers = null

currentViewers = ["jane", "nick"]

currentViewers = null

if (currentViewers) {
    // do something , e.g. notify the live streamers
    console.log("we have viewers")
}
```


```js
let currentViewers = ["jane"]

console.log(currentViewers[5])
```

```js
console.log(  Boolean("")   ) // false
console.log(  Boolean("0")  ) // true
console.log(  Boolean(100)  ) // true
console.log(  Boolean(null) ) // false
console.log(  Boolean([0])  ) // true
console.log(  Boolean(-0)   ) // false
```

whenever we are fetching something from the network/storage, we need to make sure the data is fetched successfully.
Thus, we need to use truthy and falsy values to check if we fetched the data successfully.

```js
let leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    renderLeads()
}
```

# dblclick
```js
deleteBtn.addEventListener("dblclick", function() {
    console.log("double clicked!")
})
```

this event listener will be used add double click to any item.


# Arguements vs parameters
![[Pasted image 20221206045818.png]]
```js
//.                parameters
function greetUser(greeting, name) { 
    welcomeEl.textContent = `${greeting}, ${name} 👋`
}

//.        arguments
let hi = "Howdy"
greetUser(hi, "James")
```

Its a bit tricky to remember .

https://typealias.com/guides/parameters-arguments/

# Arrays as parameters
we can pass any object as parameter.
even array and functions.



# let vs Const
`let` variables are the ones which will be reassigned
`const` are the ones which wont be reassigned.
>By using this practice , we can improve the readability  of the code, telling other programmers that which variable is a reusable one and which is not. This'll force us to think hard before we go on declaring variables.

# item.toFixed(num)
`item.toFixed(2)` will make the decimals fixed to 2 digits.

# Number
we can use `Number()` to convert string into number.
alternative to [[Scrimba frontend dev career path#Type casting]]
```js
const totalPrice = "420.69235632455"
const btn = document.getElementById("buy-btn")
btn.textContent = `Buy €${ Number(totalPrice).toFixed(2) }`
```


# Semantic HTML
instead of using div for everything, we need to proper html tags
![[Pasted image 20221206093807.png]]
![[Pasted image 20221206093817.png]]

# strange begaviors of margins
![[Pasted image 20221206094350.png]]
>this is not for flexbox as they deal with margins differently



# CSS PseudoClasses
https://www.w3schools.com/css/css_pseudo_classes.asp
[[Pseudoselectors]]

# organizing css file
body selectors at top,
element  selectors next
semantic html elements next
custom classes/ids next

try to keep the order of css items same as webpage for easy readability and debugging.

Write DRYer Code.

# CSS specificity
[[specificity while using selectors]]

CSS works on points
![[Pasted image 20221207054344.png]]
![[Pasted image 20221207054354.png]]

# Compound selectors
[[CSS selectors]]
[[CSS advanced selectors]]

# compound selectors and Specificity
we need to use css Points [[Scrimba frontend dev career path#CSS specificity]]

==we can add the points to get specificity on compound selectors==

```css
section .ad-container #req-list ul li {
    color: green; /*113 Points*/
}

body section .ad-container div .general-list li{
    color: red; /*24 Points*/
}
```
Thus the color green will win(selected).

>Dont try to over complicate compound selectors because it comes with lot of compications when it comes to specificity.

# how do you debug specificty
![[Pasted image 20221207055330.png]]
use dev tools, it'll display wwhat css property was used and what was ignored.

# Links vs Buttons
![[Pasted image 20221207055437.png]]

>we can use CSS to make links look like buttons if needed.

make the link display to inline-block and set the padding and margin.
==not width and height==



# Block vs inline vs incline block


![[Pasted image 20221207055859.png]]
![[Pasted image 20221207055915.png]]
![[Pasted image 20221207055928.png]]
> we can use this `display` property when we want to coontrol height and margin of an inline element by making it as `inline-block`

# multiple classes on same element.

we can use this method to write DRYer CSS code.

```css
.price{
    font-weight: bold;
    padding: 5px;
    margin-top: 20px;
    border-radius: 2.6px;
}

.price-up{
    box-shadow: 0px 0px 3px #4CBB17;
    color: #4CBB17;
}

.price-down{
    box-shadow: 0px 0px 3px red;
    color: red;
}

.price-equal{
    box-shadow: 0px 0px 3px #999;
    color: #333;
}
```

```html
<div class="price price-up"><p>+31.58 (3.23%)</p></div>
<div class="price price-down"><p>−0.81 (0.48%)</p></div>
<div class="price price-equal"><p>−64.51 (2.52%)</p></div>
```

# Positionining items using CSS
## Margin auto in a flex container
![[Pasted image 20221212061600.png]]
we can use the margin properties to position the element inside an flexbox container in 9 positions.

>Logic is that the margin auto will push the element in the opposite direction .

## CSS Position property
we can use this to position item
![[Pasted image 20221212062116.png]]

![[Pasted image 20221212062201.png]]

If we make an element position as absolute, it'll look for a parent container which has property set as relative.
Thus, in our code, the parent container is set as relative and the child container is set as absolute.
we can use.
>make sure you have a parent element

```css
.temperature {
/*
Challenge:
1. Position the temperature div 
   next to the sun emoji. 
*/
    position: absolute;
    top: 20px;
    left: 160px;
    /* bottom: 160px;
    right: 95px; */
    font-size: 20px;
}
```


![[Pasted image 20221212062609.png]]

# gap property in flexbox
we can use gap property in flexbox to maintain a fixed gap between items in flexbox.
This gap will not change with screen width.

![[Pasted image 20221212063358.png]]

# white space below inline elements
in the above image, you can see there's a gap below image, its not coming from any of the margins.
this is because img is inline element by default and it has a margin below it.
same applies for all inline elements.

we need to set the display tp block to eliminate this space.

```css
.item-img {
/*
Set the Display to Block
*/
    display: block;
    width: 100%;
}

```

# align-self
we can also use align-self just like how we used margin property to position items inside a flex container.
align-self looks more of a semantic way of describing the position with respect  to flexbox container.

![[Pasted image 20221212063935.png]]
![[Pasted image 20221212063958.png]]

# position fixed
to position the element relative to the window.
>this is how pop ups work
![[Pasted image 20221212064244.png]]
## position absolute vs fixed
![[Pasted image 20221212064429.png]]
to position the chat icon to the bottom right of the window:
![[Pasted image 20221212064731.png]]



Centre modal as popup fixed to centrer:
```css
.pop-up{

/*fixed position to window and define its position to centre*/
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    /* set color and width to the box*/
    background-color: deeppink;
    color: whitesmoke;
    width: 280px;
    height: 150px;
    padding: 25px; 
    border-radius: 5px;
    box-shadow: 0px 0px 20px 1px #666;
}
```

---

# Essential Js concepts - - Tom chant
![[Pasted image 20221212092125.png]]


# setTimeout
it is more like delay.
```js
console.log('What is the capital of Peru?')

setTimeout(function(){
    console.log('Lima!')
}, 3000)

setTimeout(function(){
    console.log('Ready for next question?')
}, 6000)
```

it takes two arguements 
1. function
2. time in milliseconds

# element.style

we can style property  of an element and change
```js
const revealBtn = document.getElementById('reveal-btn')
const answer = document.getElementById('answer')
const question = document.getElementById('question')

revealBtn.addEventListener('click', function(){
    answer.style.display = 'block'
    question.style.color = '#1434A4'
    question.style.backgroundColor = '#68e1fd'
    revealBtn.style.display = 'none'
})
```

> Note that when we are accessing properties using Js objects, we cannot use `-` in keys, so we need to convert the names to ==**camelCase**== 
> `background-color` is converted to `backgroundColor`

# avoid creating consts if not necessary
```js
setTimeout(function(){
        const uploadText = document.getElementById('upload-text')
        uploadText.innerText = `Making the sale...`
    }, 1500) 
```

The above code can be boiled down to single line:
```js
setTimeout(function(){
        document.getElementById('upload-text').innerText = `Making the sale...`
    }, 1500)
```


# Forms
forms live inside form tags

## inputs
- forms need input tags
	- 
https://www.w3schools.com/html/html_form_input_types.asp
	- input tags need labels
	- we can use `for` attribute on label field to link the label to its input field. for this to work, we need the id of input field and that should be assigned to the `for` attribute
	- we can click on the label and the cursor will be focused on the respective label
	- input tags need `name` which helps while retrieving the data from that input field on submission event.
	- `placeholder` attribute can be used to display hint text when the input field is empy.

```html
            <form>
                <label for="astronautName">Astronaut Name 👩‍🚀</label>
                <input 
                    type="text" 
                    id="astronautName" 
                    name="astronautName"
                    placeholder="Neil Armstrong"
                    >
            </form>

```
![[Pasted image 20221212094655.png]]




## form submission
==any button inside the button will act as submit button.==
all n number of buttons inside the form will act as submit buttons.
we can change this behavior by changing the type of button.
we can create button in 2 ways:
```html
<input type="submit">
<button>submit</button>
<button type="submit">submit</button>
```
input type submit will add a submit button.
onClick, the submit button will refresh the page by default action.

### prevent default behavior of form
```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()
})
```

## form validation
form validation can be done by setting attributes on input fields
`required` --> makes the field mandatory before submission.



## formData
![[Pasted image 20221212101140.png]]
```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()
    
    const loginFormData = new FormData(loginForm)
    console.log(loginFormData)
})
```
### formData.get()
we can use get method to get the values inside the form using names as arguements to get method.


```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()
    const loginFormData = new FormData(loginForm)
    
    const name = loginFormData.get('astronautName')
    const email = loginFormData.get('astronautEmail')
    const password = loginFormData.get('astronautPassword')
    console.log(name, email, password) 
    
/* 
Challenge: 
1. Log out the email and password from loginFormData.
*/


})
```

## disabled attribute
its a html attribue, it'll disable the button.
if we want to modify this attribute using html, we need to assign a boolean value to it
![[Pasted image 20221212102659.png]]

# reversing elemets in flexbox
```css
	flex-direction:row-reverse; /* */
```

## toggling classes using Js
```css
.container{
    display: flex;
    gap: 1px;
    justify-content: center;
    margin-top: 40px;
    margin-bottom: 40px;
}

.reverse{
    flex-direction: row-reverse;
}
```

```js
const sortBtn = document.getElementById('sort-btn')
const container = document.getElementById('container')
                  
sortBtn.addEventListener('click', function(){
    container.classList.toggle('reverse')
})

```

# aria-label for accessibility

those who are using screenreader, this field will assist them.
https://youtu.be/Jao3s_CwdRU

```html
form id="consent-form">

				<input 
					type="text" 
					name="fullName" 
					placeholder="Enter your full name"
					aria-label="Full name" 
					required/>
				<input 
					type="email" 
					name="email" 
					placeholder="Enter your email"
					aria-label="Email address" 
					required/>
```

# meme picker
![[Pasted image 20221213103844.png]]

# for of loop
```js
function getEmotionsArray(cats){
    const emotionsArray = []
    for (let i = 0; i < cats.length; i++){
        for (let j=0; j < cats[i].emotionTags.length; j++){
                emotionsArray.push(cats[i].emotionTags[j])
        }
    }
console.log(emotionsArray)
}

getEmotionsArray(catsData)
```

this way of looping works, but it makes the code look ugly, thus we can use `for of` loop to make the code more readable.

```js
    const emotionsArray = []
    
    for (let cat of cats){
        for (let emotion of cat.emotionTags){
            emotionsArray.push(emotion)
        }
        
    }
    console.log(emotionsArray)
}

getEmotionsArray(catsData)
```



[can arrays be const?](https://stackoverflow.com/posts/61517230/timeline)

Declaring a variable as `const` only means that you cannot assign a new value to that variable once a value has been assigned:

```javascript
const array = [];

array = []; // Not allowed: assignment to constant variable
```

Declaring an array as `const` has no bearing on what you can do with the contents of the actual array:

```javascript
const array = [];

array.push("something"); // Allowed: add value to array
array[0] = "or other";   // Allowed: replace value in array
array.length = 0;        // Allowed: change array size
```


# import and export modules
we can export the members in this way, so that it can be used by other modules
```js
//data.js
export const dinnerPartyGuests = [
    'Elvis Presley', 
    'The Queen of England',
    'Alan Turing', 
    'Nelson Mandela', 
    'Mahatma Gandhi', 
    'Aristotle',
    'Albert Einstein'
    ]

```

we can import items using this syntax.
inside flower brackers, we can decide to import only required things
```js
//index.js
import { dinnerPartyGuests } from '/data.js'

console.log(dinnerPartyGuests)

```
and in html, we can link the js file.
>note that the script tag must be of type ==module== to import index.js file to work as a module.


```html
<html>

	<head>
	</head>
	
	<body>
		<script src="index.js" type="module"></script>
	</body>

</html>
```



# radio inputs
```html
<div class="radio">
					<input 
					type="radio"
					id="horses"
					value="horses"
					name="choice-radios"
					>
					<label for="horses">5 duck-sized horses</label>
                	<!-- radio here -->
				</div>
```
![[Pasted image 20221215081228.png]]
note that by default the radio does not have any display value.
thus we added a lable lor it.

#todo 
- [ ] name property inside the radio input types


# inlcudes()

![[Pasted image 20221215081630.png]]
its similar to `contains` in other languages or `in` keyword in python.
>we can use this on array.

returns boolean value.


# event.target.id
to keep track of where we fot the event from.
![[Pasted image 20221215082240.png]]
we can fetch the id of target element where there event originated from.

This'll work for any element clicked inside the container. so be careful.

# .parentElement
to access the parent when you have the child.
![[Pasted image 20221215082704.png]]
we can change the style on the parent when child is changed.


# classlist add/remove
to add and remove the class to an element.
```js
document.addEventListener('click', function(e){
/*
Challenge:
1. Remove the "unread" class from the 
   parentElement of the clicked element.
*/
    document.getElementById(e.target.id).parentElement.classList.add('read')
    document.getElementById(e.target.id).parentElement.classList.remove('unread')
})
```

## accent-color
we can use this to change the color of radio button.

# getElementsByClassName
![[Pasted image 20221215083320.png]]

```js
clearBtn.addEventListener('click', function(){
/*
Challenge:
1. Finish setting up this array of 
   elements with the "product" class.
2. Iterate over this array and remove 
   the "purchase" class and add the 
   "on-offer" class.
*/
    const productsArray = document.getElementsByClassName('product')
    for (let product of productsArray){
        product.classList.remove('purchased')
        product.classList.add('on-offer')
        
    }
})

```

we can get all classes and loop through those and do our operations.


# querySelector
its more powerful way of selecting elements

```js
// We can much more easily target pseudo elements like :checked
const submitBtn = document.getElementById('submit-btn')

submitBtn.addEventListener('click', function(){
    const checkedRadio = document.querySelector('input[type="radio"]:checked')
    console.log(checkedRadio.value)
})

```

# checkboxes
to get true/false value from the user.
```js
const continueBtn = document.getElementById('continue-btn')
const acceptTerms = document.getElementById('accept-terms')
const acceptMail = document.getElementById('accept-mail')

continueBtn.addEventListener('click', function(){
    
/*
Challenge:
1. Add a second checkbox to see if a user
   wants to be added to the mailing list.
2. If they do, log out "mail accepted" when 
   the continue button is clicked. If they
   don't, log out "mail not accapted."
*/
    if (acceptTerms.checked){
        console.log("Terms accepted!")    
    }
    else{
        console.log("Terms refused!")         
    }
    
    if (acceptMail.checked){
        console.log("Mail accepted")
    }
    else{
        console.log("Mail refused")
    }
    
})
```

we can see if the checkbox is checked using `checked` property.



# array.filter()
to get only the elements we want from an array.

filter takes a function as input.

```js
const ages = [1, 5, 9, 23, 56, 10, 47, 70, 10, 19, 23, 18]

const adults = ages.filter(function(age){
    if (age >= 18){
        return true
    }
    else {
        return false
    }
})

console.log(adults)
```

```js
const ages = [1, 5, 9, 23, 56, 10, 47, 70, 10, 19, 23, 18]

const adults = ages.filter(function(age){
/*
Challenge:
1. Get rid of the if statement and reduce the 
   logic in this function to just one line 
   of code.
*/
    return age >= 18
})

console.log(adults)
```


# TextArea
```html
<textarea 
                    placeholder="Ask me anything!" 
                    id="chat-input"></textarea>
```

![[Pasted image 20221216092450.png]]
This'll give a editable text area.
>to display the placeholder, we need should have anything inside the tag. not even a single space.

```html
<textarea 
                    placeholder="Ask me anything!" 
                    id="chat-input">random text</textarea>
```
the above random text will be populated inside text area. thus removing the placeholder.
if we add a space also it'll remove the placeholder.

![[Pasted image 20221216093014.png]]
by default , text idea will be resizeable by user.
we can disable that feature using css.

**==`resize: none;`==**

```css
textarea{
    border: none;
    padding: 10px;
    margin: 0 0 20px 0;
    height: 60px;
    width: 100%;
    font-size: 20px;
    line-height: 30px;
    resize: none;
}
```



# forEach()
we can use this method to iterate over the array instead of writing a `for of` loop.
```js
const characters = [
    {
        title: 'Ninja',
        emoji: '🥷',
        powers: ['agility', 'stealth', 'aggression'],
    },
    {
        title: 'Sorcerer',
        emoji: '🧙',
        powers: ['magic', 'invisibility', 'necromancy'],
    },
    { 
        title: 'Ogre',
        emoji: '👹',
        powers: ['power', 'stamina', 'shapeshifting'],
    },  
    { 
        title: 'Unicorn',
        emoji: '🦄',
        powers: [ 'flight', 'power', 'purity'],
    }
]
```

```js

characters.forEach(function(character){
    console.log(character.powers)
```

we can also get index of array:
```js
characters.forEach(function(character, index){
    console.log(index)
})
```


# CDN font awesome
## CDN
![[Pasted image 20221216094235.png]]
https://cdnjs.com/ --> we can use this service to get list of cdns
## font awesome
we can use CDN of font awesome to get some fonts and icons.
https://fontawesome.com/

# icon tag
we can use `i` tag for icons
```html
<i class="fa-solid fa-retweet"></i>
```

then we can use css to define the icons.
in the above example, we are using custom class we got from fontawesome cdn for rendering the icon.


# Data attributes

![[Pasted image 20221216095332.png]]

![[Pasted image 20221216095434.png]]

```html
<i class="fa-solid fa-heart" data-heart="image-1"></i>
				<i class="fa-solid fa-share" data-share="image-1"></i>
```

```js
document.addEventListener('click', function(e) {
    if (e.target.dataset.share){
        console.log(e.target.dataset.share)
    }
    else if (e.target.dataset.heart){
        console.log(e.target.dataset.heart)
    }
/*
Challenge:
2. Make clicking on the heart icon log out
   the id of the image.
*/
})
```


# camelCase and smaller case in html and js
## in data attributes, stick to smaller case with dashes
==only worry in data attributes==
as you have noticed, we were converting names to camelCase when using in  js

![[Pasted image 20221216100113.png]]

due to this, stick to small case with dashes in html for properties.
and in Js you can use camelCase .
![[Pasted image 20221216100206.png]]



# copying arrays and objects


```js
const usersArray = [
    {
        userName: 'Tom',
        password: '123456'
    }
]

const userObj = usersArray[0]

userObj.userName = 'Wayne'

console.log(usersArray)
console.log(userObj)

//›[{userName: "Wayne", password: "123456"}]
//›{userName: "Wayne", password: "123456"}
```
![[Pasted image 20221216101509.png]]
memory is shared by  both objects  and array.
This is ==shallow copying== .

but we can use this shallow copy to
## deep copy
![[Pasted image 20221216102614.png]]

# conditionally render css
