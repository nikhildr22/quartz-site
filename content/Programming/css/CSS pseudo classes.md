It is used to defined special state of an element.
**Note** that pseudo-class names are not case-sensitive.

**Syntax:**
```css
selector: pseudo-class{
		property : value;
}
```

**Common Pseudo classes **
- `:hover`
	-->  when our mouse pointer is over it
- `:active`
	-->activated when the user clicks on it.
- `:focus`
	--> selector is used to select the element that has focus.
	The :focus selector is allowed on elements that accept keyboard events or other user inputs.
- `:visited`
	-->used to select the links which have been already visited by the user.
	
# Anchor tag pseudo classes:
```css
<style>
/* unvisited link */
a:link {
  color: red;
}

/* visited link */
a:visited {
  color: green;
}

/* mouse over link */
a:hover {
  color: hotpink;
}

/* selected link */
a:active {
  color: blue;
}
</style>
```

- `:first-child`
	--> selects only the first childs

link: https://www.w3schools.com/css/css_pseudo_classes.asp