by [Gill Cleeren](https://app.pluralsight.com/profile/author/gill-cleeren)
Pluralsight

---
# Getting to know bootstrap
![[Pasted image 20210410100153.png]]
Mobile first approach is of great importance now
![[Pasted image 20210410100252.png]]
![[Pasted image 20210410100356.png]]
[[jQuery]] 
## Building blocks of Bootstrap
![[Pasted image 20210410100453.png]]
all browsers support bootstrap
IE-3 supports only BS 3

# adding BS to a site
![[Pasted image 20210410100741.png]]
CDN --> content delivery network--> getting from network as static files
![[Pasted image 20210410100757.png]]
this is the precompiled version and it is ready to use.

1. goto BS site and download
2. unzip
3. you'll most likely need bootstrap.css file for this course
4.

Jumbotron is a big banner.

make sure you browse bootstrap official documentation and you can also get free templates there

# Page layout using a Grid in BS
## understadning grid
![[Pasted image 20210410103118.png]]
it was when the html started, they used tables to displaying data
disadvnatages of tables: 
![[Pasted image 20210410103219.png]]
![[Pasted image 20210410103239.png]]
![[Pasted image 20210410103312.png]]
![[Pasted image 20210410103340.png]]
![[Pasted image 20210410103351.png]]
its not just 2 cols,
![[Pasted image 20210410103427.png]]
comes with 5 widths:
![[Pasted image 20210410103438.png]]
example:
![[Pasted image 20210410103542.png]]
![[Pasted image 20210410103617.png]]
we can also control how the layout will look in the different screen sizes
![[Pasted image 20210410103739.png]]
![[Pasted image 20210410103752.png]]
![[Pasted image 20210410103813.png]]
offset -> gap
![[Pasted image 20210410103827.png]]
## applying grid
just `col` will divide up everything equally,  until 12 cols, laterly added cols will be stacked to next breakline.

>container will create centered container

then we can add cols, then rows, and these elements can be nested.

# adding style with bootstrap
## Working witrh text and typography
![[Pasted image 20210410112320.png]]
`Display-x` --> it can be applied on any text, it makes them appear larger/smaller than they should be.
bootstrap makes Headiing elements look different.
![[Pasted image 20210410112412.png]]
![[Pasted image 20210410112452.png]]
==These inline tags are exclusive provided by bootstrap.==
![[Pasted image 20210410112608.png]]


## Bootstrap for content elements
### tables in BS
`table` class --> bootstrapify the table.
`table-dark`--> makes the table dark
`<thead class="thead-light"`--> makes the table header lighter.
`table table-striped`
`table-hover` `table-bordered`
you can also change the color of particular row, column.
but the table is not responsive b itself,
so, you have to encapsulate your `table` element inside a `div.table-responsive`
### Images
adding responsive to images
`img-fluid` --> makes the image responsive
`rounded`--> rounded corners
### spacing in bootstrap
padding and margin
![[Pasted image 20210421043444.png]]
convention:
![[Pasted image 20210421043512.png]]
![[Pasted image 20210421043545.png]]
the values are in `rem`
`mt-3`/`mb-3`--> 3rem margin on top/bottom
`my-3`--> 3rem margin on Y axis
`mr-3`/`ml-3`-->3rem margin on right/left
`mx-3`-->3rem margin on X axis

>same convention for padding




# bringing functionality using Bootstrap components

## understanig components
these are ready-made building block
![[Pasted image 20210421044335.png]]
![[Pasted image 20210421044428.png]]
these are few important components.
make sure you read the documentation for each component.
Ex: 
![[Pasted image 20210421044548.png]]
==Explore these on own==
## built in components
### Jumbotron
it'll be at top of page
jumbotron should be out of container.
for adding a background image, we have to write custom css.
### Nav and navbar
nav will be in the header of the page
![[Pasted image 20210421050039.png]]
this is basic navigation.
>But we need `navbar`

![[Pasted image 20210421050130.png]]
adding style to navbar:
![[Pasted image 20210421050230.png]]
`navbar-brand`--> adds a image for the navbar

# Bootstrap form component
>forms in bootstrap are components too

## Creating a form
![[Pasted image 20210421050644.png]]
`form-group`--> groups the form elements by adding margins.
we can add forms in rows/columns /nested
![[Pasted image 20210421051020.png]]
![[Pasted image 20210421051057.png]]
![[Pasted image 20210421050712.png]]
![[Pasted image 20210421050747.png]]

## applying styles to forms inputs
we'll use `form-control` class
![[Pasted image 20210421051144.png]]
![[Pasted image 20210421051152.png]]
![[Pasted image 20210421051225.png]]
![[Pasted image 20210421051304.png]]

==you can enhance all the form components, make sure you browse the documentation.==

# Making Pages Interactive with JavaScript-enabled Components

we use Js for interactivity.
but using bootstrap, we need just basic Js.
![[Pasted image 20210421052056.png]]
![[Pasted image 20210421052134.png]]
## Carousel
scrolling images automatically after few seconds
![[Pasted image 20210421052251.png]]
![[Pasted image 20210421052342.png]]
![[Pasted image 20210421052510.png]] add these at the end.

## Dropdown
this is for dropdown menu to show a list of links.
## Dialogs
# Final Notes
this is just a intro, explore it more.
