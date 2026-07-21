link: https://www.youtube.com/watch?v=YFlx1C8XwR0
---
codewithHarryYT

goto jquery and download the uncompressed development version of jquery only if you want to read the jquey code.

download compressed version for lightwirght code.
download and place it in Js folder of your html app page.

include the script in `<head>`

or you can include the web link.
# to check if jQuery is loaded
![[Pasted image 20210422120931.png]]
`$` only works if jQuery is successfully loaded.
or else it'll throw an error.

# CDN
it'll serve jquery on network
search for jquery cdn,and include that cdn inside the html file.

there are multiple cdn's

# syntax
```js
$('selector').action(ToDoFUnction(){
					 });
```

![[Pasted image 20210422121449.png]]

# document ready
js runs only after complete loading of page doc
```js
$(document).ready(function(){
	//our jQuery code
})
```
>`$(document).ready` is same as `$`, but dont use just `$`, follow the conventions.

# 3 main types of selectors
- element
```js
$('p').click(function(){});
```
- class
```js
$('.className').click(function(){});
```
- id
```js
$('#idName').click(function(){});
```

# other selectors
`$('*').click()`--> selects everything
`$('p.className').click()`
`$('p:first').click()` --> selects first p.

# events in jQuery
## Mouse events
- click
- dblClick
- mouseEnter
- mouseLeave
## keyboard events
keypress, keydown, mediakeystatusmap
## form events
submit, change, focus, blur
## document/window events
load, resize, scroll, unload.

# ajax jQuery
data fetching and updating dom without refreshing the page.
`$.get(url, function(data, status){
alert(data);})`

`.post(url, {parametersJson}, function(data, status){alert(status)});`


