# understanding flexbox
link: https://www.youtube.com/watch?v=siKKg8Y_tQY
![[Pasted image 20210318043704.png]]
this is the basic flex, by using display flex we can make the parent a flex container.
then once its done we can add more properties.
![[Pasted image 20210318043831.png]]
these are parent properties.
we can also add properties to child items/flex items-
![[Pasted image 20210318043914.png]]
generally the code will look like this:
![[Pasted image 20210318044008.png]]
now we work on only parent container.
if we add diplay:flex in css
![[Pasted image 20210318044205.png]] oit'll look like this and 
the boxes are flexible and they contract with the screensize and they can expand upto their max defined width
![[Pasted image 20210318044319.png]]

if we make dispaly:inline-flex
now, the perent will behave like inline flex, i.e, the parent will shrink or expand, but the flex elements will wont be contract or expand.
but we dont need that!!
![[Pasted image 20210318044601.png]]

another property
`flex-flow : row rowrap`
this is combination of 2 properties, 
flex-direction and flex-wrap
but you can use it in one property itself.
![[Pasted image 20210318044748.png]]
its the default values.
if we make it `wrap` , it'll let us wrap items, the width will be preserved, but it'll go to the next line to do that
![[Pasted image 20210318045006.png]]
you can notice the hight is decreased but you can change that too.
if we do `wrap-reverse`
![[Pasted image 20210318045109.png]]
the direction of wrapping will be reversed.
`flex-direction:row`
if you change it to column
![[Pasted image 20210318045209.png]]
now the width is maximum acc to screen size and it decreases as we decrease the screen size.
the it cant go below the minimum value defined.
![[Pasted image 20210318045357.png]]

`row-reverse`
`column-reverse`

# main axis vs cross axis
![[Pasted image 20210318045639.png]]
![[Pasted image 20210318045925.png]]
row is the default value.

`align-items:streth`
![[Pasted image 20210318050213.png]]
`align-items:center`![[Pasted image 20210318050241.png]]
![[Pasted image 20210318050303.png]]
this is only relating to the cross axis(and not related to height or width), they'll just be aligned to the center of the cross axis.
`align-items:flex-start`
![[Pasted image 20210318050449.png]]
it'll align items to the cross axis.

property:
 `justify-content:center`
 this is centering along the main axis.
 ![[Pasted image 20210318050651.png]]
 `flex-end` ![[Pasted image 20210318050727.png]]
 flex-start ![[Pasted image 20210318050809.png]]
 (this is with modified height of parent)
 # align-items and justify content
 ![[Pasted image 20210318050928.png]]
 ![[Pasted image 20210318050945.png]]
 go to mdn rerence ![[Pasted image 20210318051029.png]]

property:
`align-content:center`
#assignment 
mdn flexbox(experiment with it)

---

# working with flex items
now that we are done with parent, to modify the items, we have to add properties to child elements.
`order:0`--> default ![[Pasted image 20210318051915.png]]
we can order the items according to their positions

property: `align-self:flex-start`
this is in relation to cross axis.
![[Pasted image 20210318052220.png]]
![[Pasted image 20210318052240.png]]
for `flex-end`
![[Pasted image 20210318052255.png]]


property: `flex:0 1 auto`
this is combiantion of 3 properties
flex-grow and flex-shrink and flex-basis
making `flex-grow` to 1, the item grows till the entire empty space is occupied.
the value has to be greater than 0.

since each item can have seperate grow value, we can control how much each item grows, by specifying different grow values to different itrems
`flex-shrink` --> this will control the relative shrink value, you can have different shrink values for different items.
`flex-basis:auto`--> defines the starting the starting size of the element relating to the main axis.
![[Pasted image 20210318053611.png]]
this'll change the size related to main axis.
==dont think in terms of height and width, think of main and cross axis==
