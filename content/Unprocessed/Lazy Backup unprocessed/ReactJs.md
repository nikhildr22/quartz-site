# 1
need to brush up js,es6,css,html

# 2 what we'll learn
- learn to think in syntax.
- declarative vs impleretive programming
- JSX
- Custom components
- CSS styling

# First react
use the react cdn
and use babel cdn to use some features of react
```html
<html>

<head>

<link rel="stylesheet" href="index.css">

<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>

<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>

<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

</head>

<body>

	<div id="root"></div>
	
	<script src="index.js" type="text/babel"></script>

</body>

</html>
```

```js
ReactDOM.render(ReactDOM.render(<h1>Hello, everyone!</h1>, document.getElementById("root"))
```



# first react practice
rendering a unorder list using react.

# local setup
download as zip and use it in your local, use live server plugin in vs code

# Why React? Its COmposable
small pieces of code to instead of one big piece of html code.

## Web Components
![[Pasted image 20220806110015.png]]

```js
  

function MainContent() {

return (

<h1>I'm learning React!</h1>

)

}

  

ReactDOM.render(

<div>

<Navbar />

<MainContent />

</div>,

document.getElementById("root")
```

# WHy react? Its declarative.
![[Pasted image 20220806110226.png]]
![[Pasted image 20220806110437.png]]

# JSX
Javascript XML
this helps us make the javascript declarative.

JSX converts html code directly into object nodes which are json objects with bunch of properties.

for instead of writing all the lines of code just to create a element, we can just go ahead and write the actual html code and the JSX will do the job of converting them into DOM object with a bunch of properties.


# Good by CDN
we'll remove CDN and Babel
// NOTE: this is how you remove CDNs and Import react into your index.js

// This import has to be done because, previously the CDNs were providing global access to the libraries. But if we are adding libraries by ourselves, we need to import them

// here we are importing react and reactDOM


# react 18, createRoot API
This course uses react 17, but in react 18, we need to create root element using this syntax

Then we can render inside this root object

# 11. Thought experiment: use .append() instead of ReactDOM.render()?
![[Pasted image 20220806113412.png]]
jsx returns object, thus we cant append.
instead, if we use react:
![[Pasted image 20220806113508.png]]

# 12. Project part 1 - markup
Just basic practice of react

# 14. Custom Components
so far we've declared variables containing jsx code.
But almost as similar to traditional html code.
Thus we need custom components to simplify this.

To create custom components, we need to create funtion like code blocks.
standard conventions:
- Component name should be PascalCase
- instead of using `MyComponent()` to call the component, we'll use `<MyComponent />`

![[Pasted image 20220806123930.png]]

>function that returns react elements is called a react component


# 15. Custom Components part 2
created another custom component

# 17. Parent/Child Components
its not a good practice to put everything into a one big component.
Thus we'll create child components
Its just like modular approach of functions.

# 18. Styling with Classes
to define class on element, we need to use `className` instead of `class`, because there are dom objects. and the property name is className.

using this class name, we can add any style using css. 

# 19. Organize components
Best practices to organize components.
![[Pasted image 20220806130705.png]]
![[Pasted image 20220806130718.png]]

Move the Component to its own js file.
then make it accessible from other code by using export option.
Then import the code in index.js file

![[Pasted image 20220806130914.png]]
--> this'll be final cleaned component


# 21. Quick mental outline of project

![[Pasted image 20220822052609.png]]
the above layout can be done in the below way
![[Pasted image 20220822052518.png]]


# Project setup

Create `components` folder
keep all your component files there.

Then import those component files in your `App.js` file

Then import the `App.js` file in `index.js`

```jsx
//Navbar.js
import React from "react"

  

export default function Navbar() {

		return <h1>navbar component</h1>

}
```

```jsx
//Main.js
import React from "react"

  

export default function Main() {

		return <h1>Main component</h1>

}
```


```jsx
//App.js
import React from "react"

import Navbar from "./components/Navbar"

import Main from "./components/Main"

  

export default function App() {

return (

	<div className="container">
	
		<Navbar />
		
		<Main />
	
	</div>

)

}
```

```jsx
//index.js
import React from "react"

import ReactDOM from "react-dom"

import App from "./App"

  

ReactDOM.render(<App />, document.getElementById("root"))

```

Get google fonts in html file
```html
<html>

	<head>
	
		<link rel="preconnect" href="https://fonts.googleapis.com">
		
		<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
		
		<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
		
		<link rel="stylesheet" href="style.css">
	
	</head>

	<body>
	
		<div id="root"></div>
		
		<script src="index.pack.js"></script>
		
	</body>

</html>
```

Final file structure will look like:
![[Pasted image 20220822053847.png]]


# Figma tutorial

View only mode is best if you are  a developer and not a designer
![[Pasted image 20220822054319.png]]
turn off multiplayer cursors to avoid distractions

You can duplicate the template to your drafts if you want to make edits to the template.


## inspect panel

click on the element, the right side panel will show properties.

dont copy css as it is, as sizes might mess up. but we can use other properties.

## Export
we can export elements like logos images inside the figma file using the export window.

select the element, goto export window, export, download

we can use these files in our local project.

# 24. Navbar & Styling
for navbar, we can use `nav` element of html


# solo project
![[Pasted image 20220824062530.png]]


# airBNB site using react
1. Prop
2. creating components from array of data


# 2. Project setup: Navbar

# 
we can `{}` to use inline values/variables.

we can insert any js code inside `{}`

how to pass value using props?

# passing values is just like using html attributes.

```jsx
<Contact

img="./images/pumpkin.png"

name="Pumpkin"

phone="(0800) CAT KING"

email="pumpkin@scrimba.com"

/>
```

in this all these values are passed to the actual react component.


# how to use the passed props?

```jsx
import React from "react"

  

export default function Contact(whateverName) {

console.log(whateverName)

}
```
output:
```json
{img: 

"./images/mr-whiskerson.png"

, name: 

"Mr. Whiskerson"

, phone: 

"(212) 555-1234"

, email: 

"mr.whiskaz@catnap.meow"

}
```

this'll print out an object with all props as an object. (object and properties)

```jsx
import React from "react"

  

export default function Contact(props) {

/**

* Challenge: Fix the code below to use the `props`

* object values in place of the hardcoded values below

*/

return (

<div className="contact-card">

<img src={props.img}/>

<h3>{props.name}</h3>

<div className="info-group">

<img src="./images/phone-icon.png" />

<p>{props.phone}</p>

</div>

<div className="info-group">

<img src="./images/mail-icon.png" />

<p>{props.email}</p>

</div>

</div>

)

}
```

# destructuring props

we can use `{}` to destructure the objects.
note that the order of destrcuturing should be same in the order the props were passed.
```jsx
export default function Contact({img, name, phone, email}) {

return (

<div className="contact-card">

<img src={img}/>

<h3>{name}</h3>

<div className="info-group">

<img src="./images/phone-icon.png" />

<p>{phone}</p>

</div>

<div className="info-group">

<img src="./images/mail-icon.png" />

<p>{email}</p>

</div>

</div>

)

}
```

we can any of these methods to pass the props.


# what if the props were not passed?

lets say the `props.setup` was not passed, but the react will render empty `h3` that'll consume space.

```jsx
export default function Joke(props) {

	return (
	
			<div>
			
				<h3>{props.setup}</h3>
				
				<p>{props.punchline}</p>
				
				<hr />
			
			</div>
	
	)

}

```
Thus, we need to chcek conditions using jsx syntax: 
```jsx

export default function Joke(props) {

	return (
	
		<div>
		
			{props.setup && <h3>Setup: {props.setup}</h3>}
			
			<p>Punchline: {props.punchline}</p>
			
			<hr />
		
		</div>
	
	)

}
```


we'll use another set of curly braces, and within that we'll have a condition..

another method is by using css conditionally:
```jsx

<h3 style={{display: props.setup ? "block" : "none"}}>Setup: {props.setup}</h3>
```



# we can pass any non string value to a prop
we use `{}` to pass in any other value which is not a string.

we can pass any value supported by js.
it can be a object or any other compuattion inside the `{}`


passing image name, but appending path at component level

```jsx

<img src={`../images/${props.img}`} className="card--image" />
```


- [ ] js map function on an array [[javascript|js]]
- [ ] spread in object literals https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals

for passing props, we can deconstruct and then pass
or
pass entire objects
or
spread the props and pass

its a personal preference.



# solo project  - travel journal
![[Pasted image 20220829094610.png]]


# meme generator
![[Pasted image 20220829212149.png]]
![[Pasted image 20220829212201.png]]

https://www.figma.com/file/MoLwFPHNHJVrzdFurxHzNV/Meme-Generator

![[Pasted image 20220905042607.png]]

# header

- [ ] learn CSS grid

- [ ] why rem for fonts instead of pixes and how to do it


# react mouse events

https://reactjs.org/docs/events.html#mouse-events


# difference between props and state

props are paramenters
props are immutable, should not be changed inside the component body.

states are defined in the component and is changing.

React components has a built-in `state` object.

The `state` object is where you store property values that belongs to the component.

When the `state` object changes, the component re-renders.

1. How would you describe the concept of "state"?
A way for React to remember saved values from within a component.
This is similar to declaring variables from within a component,
with a few added bonuses (which we'll get to later)


2. When would you want to use props instead of state?
Anytime you want to pass data into a component so that
component can determine what will get displayed on the
screen.


3. When would you want to use state instead of props?
Anytime you want a component to maintain some values from
within the component. (And "remember" those values even
when React re-renders the component).


# useState

it is one of the react hooks methods.

```jsx

import React from "react"

  

export default function App() {

/**

* Challenge: Replace our hard-coded "Yes" on the page with

* some state initiated with React.useState()

*/

const result = React.useState("Yes")

console.log(result)

return (

<div className="state">

<h1 className="state--title">Is state important to know?</h1>

<div className="state--value">

<h1>{result[0]}</h1>

</div>

</div>

)

}
```

![[Pasted image 20220905050105.png]]

# useState Array destructuring
```jsx

import React from "react"

  

export default function App() {

const [isImportant, func] = React.useState("Yes")

console.log(isImportant)

return (

<div className="state">

<h1 className="state--title">Is state important to know?</h1>

<div className="state--value">

<h1>{isImportant}</h1>

</div>

</div>

)

}
```

instead of descructuring while rendering, we can destructure using  the useState method.

# changing state
```jsx
import React from "react"

  

export default function App() {

const [isImportant, setIsImportant] = React.useState("Yes")

/**

* Challenge:

* 1. Create a function called `handleClick` that runs

* setIsImportant("No")

* 2. add a click event listener to the div.state--value

* that runs `handleClick` when the div is clicked.

*/

function handleClick() {

let n = Math.random()

setIsImportant(`${Math.floor(n*100)}`)

}

return (

<div className="state">

<h1 className="state--title">Is state important to know?</h1>

<div className="state--value" onClick={handleClick}>

<h1>{isImportant}</h1>

</div>

</div>

)

}
```

```jsx
import React from "react"

  

export default function App() {

/**

* Challenge: Set up state to track our count (initial value is 0)

*/

const [isImportant, setIsImportant] = React.useState(0)

function handleClickPlus() {

setIsImportant(isImportant+1)

  

}

  

function handleClickMinus() {

setIsImportant(isImportant-1)

  

}

return (

<div className="counter">

<button className="counter--minus"

onClick={handleClickMinus}

>–</button>

<div className="counter--count">

<h1>{isImportant}</h1>

</div>

<button className="counter--plus"

onClick={handleClickPlus}

>+</button>

</div>

)

}
```

-> though this works, its not a best practice , so we've to use the best practice .


# change state using callback function
This is the best practice in react

```jsx
import React from "react"

  

export default function App() {

const [count, setCount] = React.useState(0)

/**

* Note: if you ever need the old value of state

* to help you determine the new value of state,

* you should pass a callback function to your

* state setter function instead of using

* state directly. This callback function will

* receive the old value of state as its parameter,

* which you can then use to determine your new

* value of state.

*/

function add() {

setCount(prevCount => prevCount + 1)

}

// Challenge: update `substract` to use a callback function

function subtract() {

setCount(prevCount => prevCount - 1)

}

return (

<div className="counter">

<button className="counter--minus" onClick={subtract}>–</button>

<div className="counter--count">

<h1>{count}</h1>

</div>

<button className="counter--plus" onClick={add}>+</button>

</div>

)

}
```

1. You have 2 options for what you can pass in to a
   state setter function (e.g. `setCount`). What are they?
   
a. New value of state (setCount(42))
b. Callback function - whatever the callback function 
   returns === new value of state


2. When would you want to pass the first option (from answer
   above) to the state setter function?
Whenever you don't need the previous value of state to determine
what the new value of state should be.


3. When would you want to pass the second option (from answer
   above) to the state setter function?
Whenever you DO need the previous value to determine the new value


>Note:
>The useState  should be defined at the beginning of the component.

- [ ] sizing images


# using react state with arrays
we can use array spread operator to add a new item.
note that we cant modify the state object directly, we need to use the useState methods to set the values.

and in the below example, the next value depends on the previous value of the state variable, we need to use a callback function .
```jsx

import React from 'react';

import ReactDOM from 'react-dom';

  

function App() {

/**

* Challenge: Convert the code below to use an array

* held in state instead of a local variable. Initialize

* the state array with the same 2 items below

*

* Don't worry about fixing `addItem` quite yet.

*/

const [thingsArray, setThingsArray] = React.useState(["Thing 1", "Thing 2"])

function addItem() {

// We'll work on this next

setThingsArray(prevThingsArray => {

return [...prevThingsArray, `Thing ${prevThingsArray.length + 1}`]

})

}

const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)

return (

<div>

<button onClick={addItem}>Add Item</button>

{thingsElements}

</div>

)

}

  

ReactDOM.render(<App />, document.getElementById('root'));
```

>The array spread operator can be used to return an new array with extra item added.


# using objects in state

just use dot operator .


to modify the objects:
```jsx
function toggleFavorite() {

setContact(prevContact => ({

...prevContact,

isFavorite: !prevContact.isFavorite

}))

```

Note that jsx objects are just json arrays.

so, we'll destructure  array and modify the propery we want to modify and we'll return that object.



if we want to pass the state.


# passing data to components
![[Pasted image 20220905092420.png]]

![[Pasted image 20220905092444.png]]

state can only be passed down.

we've to use react redux states to pass data between components(thats advanced)

>use bool values inside states, another othre custom objects will be updated if the state changes.


# short circuiting conditional statements in jsx
## we can use these for conditional renderinh

```jsx
import React from "react"

  

export default function Joke(props) {

const [isShown, setIsShown] = React.useState(false)

/**

* Challenge:

* - Only display the punchline paragraph if `isShown` is true

*/

function toggleShown(){

setIsShown(prevShown => !prevShown)

}

return (

<div>

{props.setup && <h3>{props.setup}</h3>}

{isShown && <p>{props.punchline}</p>}

<button onClick={toggleShown}>Show Punchline</button>

<hr />

</div>

)

}

```

we can use `&&` logical operator to do short circuiting so that the second condition will only be run if the condition  on the right is satisfied.

# conditional rendering
1. we can use `&&` if we just have a single condition
2. we can use ternary operator if we have 2 choices to choose
3. if we have multiple conditions, we can use if else ladder


# React Forms
```jsx

import React from "react"

  

export default function Form() {

const [firstName, setFirstName] = React.useState("")

const [lastName, setLastName] = React.useState("")

function handleFirstNameChange(event) {

setFirstName(event.target.value)

}

function handleLastNameChange(event) {

setLastName(event.target.value)

}

return (

<form>

<input

type="text"

placeholder="First Name"

onChange={handleFirstNameChange}

/>

<input

type="text"

placeholder="Last Name"

onChange={handleLastNameChange}

/>

</form>

)

}
```

>Note that we are using event  get the target




in this above example we have chang handler functions for every form input component.
But this is not ideal, as the size of the form grows, we have to write more handlers.

Thus we need to create a object

```jsx
import React from "react"

  

export default function Form() {

const [formData, setFormData] = React.useState(

{firstName: "", lastName: ""}

)

console.log(formData)

function handleChange(event) {

setFormData(prevFormData => {

return {

...prevFormData,

[event.target.name]: event.target.value

}

})

}

return (

<form>

<input

type="text"

placeholder="First Name"

onChange={handleChange}

name="firstName"

/>

<input

type="text"

placeholder="Last Name"

onChange={handleChange}

name="lastName"

/>

</form>

)

}

```

>Note that we are using a property as value:
we can use square braces to convert value as property in react.


```jsx

return {

...prevFormData,

[event.target.name]: event.target.value

}
```


# controlled components
```jsx

<form>

<input

type="text"

placeholder="First Name"

onChange={handleChange}

name="firstName"

value={formData.firstName}

/>
```

in the previous example, only the form was controlling react states and not vice versa.
there has to be just a single copy of truth.

thus we need to modify the code such that the react state will control the form values as well and vice versa.

- [ ] htmlFor property 

```jsx
<input

type="checkbox"

id="isFriendly"

checked={}

/>

<label htmlFor="isFriendly">Are you friendly?</label>

```

![[Pasted image 20220906055651.png]]

```jsx

import React from "react"

  

export default function Form() {

const [formData, setFormData] = React.useState(

{

firstName: "",

lastName: "",

email: "",

comments: "",

isFriendly: true

}

)

function handleChange(event) {

const {name, value, type, checked} = event.target

setFormData(prevFormData => {

return {

...prevFormData,

[name]: type === "checkbox" ? checked : value

}

})

}

return (

<form>

<input

type="text"

placeholder="First Name"

onChange={handleChange}

name="firstName"

value={formData.firstName}

/>

<input

type="text"

placeholder="Last Name"

onChange={handleChange}

name="lastName"

value={formData.lastName}

/>

<input

type="email"

placeholder="Email"

onChange={handleChange}

name="email"

value={formData.email}

/>

<textarea

value={formData.comments}

placeholder="Comments"

onChange={handleChange}

name="comments"

/>

<input

type="checkbox"

id="isFriendly"

checked={formData.isFriendly}

onChange={handleChange}

name="isFriendly"

/>

<label htmlFor="isFriendly">Are you friendly?</label>

<br />

</form>

)

}
```

in the above  example, we are using a checkbox.
unlike other input values, checkbox holds bool value.

Thus we need to destructure the event.target 
and then get the values.
and then use the ternary operator to determine the values.

```jsx
function handleChange(event) {

const {name, value, type, checked} = event.target

setFormData(prevFormData => {

return {

...prevFormData,

[name]: type === "checkbox" ? checked : value

}

})

}
```

## radio buttons in state
```jsx
import React from "react"

  

export default function Form() {

const [formData, setFormData] = React.useState(

{

firstName: "",

lastName: "",

email: "",

comments: "",

isFriendly: true,

employment: ""

}

)

console.log(formData.employment)

function handleChange(event) {

const {name, value, type, checked} = event.target

setFormData(prevFormData => {

return {

...prevFormData,

[name]: type === "checkbox" ? checked : value

}

})

}

return (

<form>

<input

type="text"

placeholder="First Name"

onChange={handleChange}

name="firstName"

value={formData.firstName}

/>

<input

type="text"

placeholder="Last Name"

onChange={handleChange}

name="lastName"

value={formData.lastName}

/>

<input

type="email"

placeholder="Email"

onChange={handleChange}

name="email"

value={formData.email}

/>

<textarea

value={formData.comments}

placeholder="Comments"

onChange={handleChange}

name="comments"

/>

<input

type="checkbox"

id="isFriendly"

checked={formData.isFriendly}

onChange={handleChange}

name="isFriendly"

/>

<label htmlFor="isFriendly">Are you friendly?</label>

<br />

<br />

<fieldset>

<legend>Current employment status</legend>

<input

type="radio"

id="unemployed"

name="employment"

value="unemployed"

checked={formData.employment === "unemployed"}

onChange={handleChange}

/>

<label htmlFor="unemployed">Unemployed</label>

<br />

<input

type="radio"

id="part-time"

name="employment"

value="part-time"

checked={formData.employment === "part-time"}

onChange={handleChange}

/>

<label htmlFor="part-time">Part-time</label>

<br />

<input

type="radio"

id="full-time"

name="employment"

value="full-time"

checked={formData.employment === "full-time"}

onChange={handleChange}

/>

<label htmlFor="full-time">Full-time</label>

<br />

</fieldset>

</form>

)

}

```

```jsx
import React from "react"

  

export default function Form() {

const [formData, setFormData] = React.useState(

{

firstName: "",

lastName: "",

email: "",

comments: "",

isFriendly: true,

employment: "",

favColor: ""

}

)

function handleChange(event) {

const {name, value, type, checked} = event.target

setFormData(prevFormData => {

return {

...prevFormData,

[name]: type === "checkbox" ? checked : value

}

})

}

function handleSubmit(event) {

event.preventDefault()

// submitToApi(formData)

console.log(formData)

}

return (

<form onSubmit={handleSubmit}>

<input

type="text"

placeholder="First Name"

onChange={handleChange}

name="firstName"

value={formData.firstName}

/>

<input

type="text"

placeholder="Last Name"

onChange={handleChange}

name="lastName"

value={formData.lastName}

/>

<input

type="email"

placeholder="Email"

onChange={handleChange}

name="email"

value={formData.email}

/>

<textarea

value={formData.comments}

placeholder="Comments"

onChange={handleChange}

name="comments"

/>

<input

type="checkbox"

id="isFriendly"

checked={formData.isFriendly}

onChange={handleChange}

name="isFriendly"

/>

<label htmlFor="isFriendly">Are you friendly?</label>

<br />

<br />

<fieldset>

<legend>Current employment status</legend>

<input

type="radio"

id="unemployed"

name="employment"

value="unemployed"

checked={formData.employment === "unemployed"}

onChange={handleChange}

/>

<label htmlFor="unemployed">Unemployed</label>

<br />

<input

type="radio"

id="part-time"

name="employment"

value="part-time"

checked={formData.employment === "part-time"}

onChange={handleChange}

/>

<label htmlFor="part-time">Part-time</label>

<br />

<input

type="radio"

id="full-time"

name="employment"

value="full-time"

checked={formData.employment === "full-time"}

onChange={handleChange}

/>

<label htmlFor="full-time">Full-time</label>

<br />

</fieldset>

<br />

<label htmlFor="favColor">What is your favorite color?</label>

<br />

<select

id="favColor"

value={formData.favColor}

onChange={handleChange}

name="favColor"

>

<option value="red">Red</option>

<option value="orange">Orange</option>

<option value="yellow">Yellow</option>

<option value="green">Green</option>

<option value="blue">Blue</option>

<option value="indigo">Indigo</option>

<option value="violet">Violet</option>

</select>

<br />

<br />

<button>Submit</button>

</form>

)

}

```

```jsx
function handleSubmit(event) {

event.preventDefault()
//preventDefault will prevent default actions on submit, aka the page will not refresh
// submitToApi(formData)

console.log(formData)

}
```



>in HTML5, the button element inside the form is by default a submit button.


SInce we've been maintaining the state all along the process of taking inputs from beginning, we dont have to gather the data on submit again.
we'll just take the data from state and use it.

we also have an onSubmit handler on form element.





