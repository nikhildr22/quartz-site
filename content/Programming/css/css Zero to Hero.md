link : https://www.youtube.com/watch?v=1Rs2ND1ryYc

---
# syllabus
prerequisite - HTML

- [[checking css on a page]]
- selectors and properties
- coloring and formatting
-  fonts and text manipulation
-  Layout
-  flexbox
-  grid
-  animations and transitions
-  challenge

git link: https://github.com/Video-Lab/css-course-content/

[[CSS selectors]]



[[specificity while using selectors]]

[[Pseudoselectors]]

[[CSS advanced selectors]]

# Properties
what are properties?
properties define the change.
`propertyName : value;` --> format

# css general rule
there are 3 parts:
```css
selector {
	//css block --> it can be empty
	property : value;
	property : value;
}
```

# types of colors
## css color codes
these are semantic names available in css.

## hex codes
start with `#` follwed by 6 digits.
`#RRGGBB`

## RGB codes
`rgb(r, g, b)`
0 to 255

use a color picker --> just google it'll make the job easier.

# coloring text
![[Pasted image 20210402113603.png]]
![[Pasted image 20210402113612.png]]
but make a preference of adding rbg code, its much easier to change
![[Pasted image 20210402113621.png]]

# background colors
we can use `background-color` 
but `background` is much more flexible as it can add color/image.
![[Pasted image 20210402114019.png]]

# images/URLs in css
css has [[css functions]]
rbg() is a function #aha 
css functions are built-in functions.

![[Pasted image 20210402114305.png]]
URL can also be a local url.

# other background properties
![[Pasted image 20210402114621.png]]
![[Pasted image 20210402114635.png]]
![[Pasted image 20210402114655.png]]
backgrond-size:
![[Pasted image 20210402114736.png]]
==repeat is the default value==
![[Pasted image 20210402114801.png]]
`cover` resizes without thinking about the quality of scaled image.

`contain` resizes only until the image quality is maintained, later it is repeated.
![[Pasted image 20210402114950.png]]

# opacity/transparancy
along with RGB values we'll add `alpha` value
it is transparacy or opaccity
0 to 1 <--> lighter to darker
this'll be in decimals.
![[Pasted image 20210402115238.png]]

# Gradients
transition between two colors
## radial gradient
circular --> color changes in the direction of radii 
they cant have background-size
![[Pasted image 20210402120138.png]]
![[Pasted image 20210402120145.png]]
if want to add proportions
![[Pasted image 20210402120209.png]]
selecting the shape:
![[Pasted image 20210402120227.png]]
by dfault it is elliptical
## liner gradient
color changes linerarly/diagonally
![[Pasted image 20210402115641.png]]
we can add as many colors we want

diagonal : ![[Pasted image 20210402115808.png]]
![[Pasted image 20210402115815.png]]
degrees:
![[Pasted image 20210402115933.png]]

# introduction to types of units
## absolute units
does not depend on other values
ex: cm. mm. inches
## relative units
these depend on parent values
ex: %, px, 
this is very good for responsive design
`px` --> it depends on the dpi.  so on high resolution devices, the pixel value changes. 

`em` --> it'll change acc to standard font size.

`vw` --> view width
`vh` --> view hight  
vw and vh can make the scale depending on the dimentions of the viewport.
![[Pasted image 20210403073334.png]]
it can start from 1 and go beyond 100(100%)
The **`vw` and `vh` units** stand for the percentage of the width and height of the actual viewport. They can take a value **between 0 and 100** according to the following rules:

100vw = 100% of viewport width
1vw = 1% of viewport width

100vh = 100% of viewport height
1vh = 1% of viewport height

**avoid absolute values as they'll be fixed and when the user changes the device, there'll be issues**

# text minipulation and font manipulation
## text minipulation
`text-decoration` --> 
`none`.`underline`, `line-through`, `overline`

`text-transform` --> `capitalize`,`lowecase`, `uppercase`

`text-align`-->this is for justification
--> `left`,`center`, `right`,`justify`

## font manipulation
this is font properties
`font-size`-->use scale values
`font-weight`--> decides the bolding of font
starts from 0 till infinity.
but most fonts have limit to bolding. 0 will be very thin.

`font-style` -->`italic`,`oblique`

## font families
`font-family`
#todo_web research about fonts(serif vs sans-serif)
-->`sans-serif`(mostly used and looks clean)
we can include muliple fonts depedning on the precedance.
![[Pasted image 20210403074734.png]]![[Pasted image 20210403074738.png]]
it needs to be mentioned in the `""`

## using external fonts
get the fonts from internet.
goto fonts.google.com
Note: ==font weightt may fail, for some custom fonts==
therefore it is recommended to choose the right font with right properties from the fonts.google site.
![[Pasted image 20210403075435.png]]
copy the link tag and paste it before the link to stylessheet
![[Pasted image 20210403075511.png]]
now use `font-family` to change the font.
using multiple fonts can make the site look lot better.
>if there's a failure in fetching font from api, add a seperate font to precedance, make sure the font is of same family to avoid the severity of of difference in looks.
>![[Pasted image 20210403075825.png]]

# CSS Layouts
## Box model

![[Pasted image 20210403075930.png]]
![[Pasted image 20210403080115.png]]
![[Pasted image 20210403080130.png]]
more room around conytent --> padding
![[Pasted image 20210403080159.png]]
![[Pasted image 20210403080214.png]]
padding --> internal space
margin --> external space	

## change content style
this the first layer of box model
`height` --> height of content
`width` --> width of content

in most of the cases, height is absollute value and width is relative, but its totally your preferrance.

## css borders
`border`--> `size style color`
this is 3 properties combined
This property is a shorthand for the following CSS properties:
1. border-color
2. border-style
3. border-width

`size` -> can be any value
`style`-->`dotted`,`dashed`, `solid`, `double`

`color`--> can be of any color.
**syntax:**
```css
/* style */
border: solid;

/* width | style */
border: 2px dotted;

/* style | color */
border: outset #f33;

/* width | style | color */
border: medium dashed green;

/* Global values */
border: inherit;
border: initial;
border: revert;
border: revert-layer;
border: unset;

```
we can also specify border on all directions, with other properties
```css
border-right
border-left-color
border-top-style
border-bottom-width
```


## margin and padding
padding --> internal space
margin --> external space
`padding: x`--> x space on all sides
`padding : x y` --> x pading on top-down and y space on right-left.
it can be `padding-X` where X can be top right bottom left.
`padding : top right left bottom right;` --> we can add padding to every side on the single line.
>**same syntax holds true for margin**

## float and display types
there are two display types :
- inline (ex/: span)
- block level(ex: p , div)

`float` --> `right` : this moves the block to the right and everything below will be pushed upward to cover up the empty space.
![[Pasted image 20210403093020.png]]
![[Pasted image 20210403093035.png]]
`display`--> other than inline and block, display can give u extra display features.
`display:`
`none`-->dissapears
`inline-block`--> inline+block  
`inline`

`float : inherit;`--> takes the float property of parent element.
`float:none`--> default and doesnt move
 
## Flexbox
![[Pasted image 20210403093756.png]]
![[Pasted image 20210403093804.png]]
![[Pasted image 20210403093818.png]]
 this makes our job of making the site responsive easier.
 
 ## creating a flex container
 
 `display : flex` --> flex mode activated.
 this should be set on parent container.
 
 ## flex direction and wrap.
 `flex-direction` --> `row`(default), `column`, `row-reverse`, `column-reverse`
 
 `flex-wrap`--> `wrap`, `nowrap`(default)
  if it is wrap, instead of adjusting the spacing, the element will move to next line.
  
  ## content alignment
  `justify-content`--> horizontal alignmet
  --> `flex-start`, `center`, `flex-end`, `space-around`, `space-between`
  
  `align-items` --> vertical property
  --> `flex-start`, `center`, `flex-end`, `baseline`, `stretch`
  
  ## flex items order
  we can add this as inline style.
  `order : `-->takes numbers and default value is 0.
  so while setting
  ![[Pasted image 20210403095146.png]]
  ![[Pasted image 20210403095152.png]]

## Shrink , Grow and basis
these are related to flexbox.
==these define the extra spaces between the flex items and how they are utilzed==
`flex-basis`--> sets the minimum width of flex item.
`flex-grow` --> determines the dynamic size of the flex item
`0`--> default
`1` to any value and this value is related to other flexgrow values.
 
 `flex-shrink`--> when it goes below minimum width of item, every item is shrinked in same rate.
 but you can give values to this property.
 if we make it `0` , it doesnt shrink
 default =  `1`
 
 ## the 'flex' property
 this is the combination of all other flex properies
 
 `flex: grow shrink basis`
  
## item alignment in flex
`align-self` --> it'll override `align-items` for that specific flex item
`align-self` --> `flex start`, `flex-end`, `center`

## Grid vs Flexbox
![[Pasted image 20210403102523.png]]
![[Pasted image 20210403102531.png]]
![[Pasted image 20210403102549.png]]
## creating a grid
`display:grid;`
in grid there are no default values, we have to set everything manually.
## Template columns and rows
`grid-templete-columns`-->  

![[Pasted image 20210403103113.png]]
![[Pasted image 20210403103141.png]]
![[Pasted image 20210403103146.png]]
auto --> divides the spaces equally.

## justify and align grid
`justify-content`-->`start`, `end`, `end`, `space-evenly`, `space-around`

`align-content`--> `space-between`, `space-evenly`,`end` etc

## row and column gaps in grid
`grid-column-gap` --> takes values
`grid-row-gap`--> takes values
`grid-gap : row column` --> takes both values at once.

## column and row lines in grid
`grid-column : start/end;`
`grid-row : start/end;`

 we can also use `span` ![[Pasted image 20210403104655.png]]
 
 ## Grid Area
 `grid-area : row_start / row_end column_start / column_end;`
 ![[Pasted image 20210403104849.png]]
 
 ## Transition Property
 #todo/paused  https://youtu.be/1Rs2ND1ryYc?t=17102
 





