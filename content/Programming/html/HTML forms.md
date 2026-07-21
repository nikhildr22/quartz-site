# html form basics
![[Pasted image 20210401052105.png]]
## using forms
form tag
action attribute --> destination
method --> http method
enctype --> encoding type
## understanding form components
## building and submitting forms
input tag with type submit
# Input types
![[Pasted image 20210401052837.png]]
![[Pasted image 20210401052849.png]]
text:
 - name--> field name, mandatory
 - name will be sent to server
 
 textarea --> large text area
 other data types:
 ![[Pasted image 20210401053939.png]]
 we can use preferred data type to get the get the data in desired format.
 ## selection inputs
 ![[Pasted image 20210401094559.png]]
 we'll get a visual indication for selection.
 ex: range
 select tag -->
 ```html
<select>
	<option></option>
</select>
```

you can select multiple items and we can also limit using attributes.

Checkbox and radio:
type="checkbox"
type="radio"
we can on make it select only one option by naming all radios with same name.
#todo_web  difference between radio and checkbox


# organizing form inputs
## grouping using fieldsets
![[Pasted image 20210401095716.png]]
![[Pasted image 20210401095725.png]]
this is just for grouping information.
`legend` tag is used inside the fieldset tag to name the field set.

## identifying with labels
![[Pasted image 20210401095959.png]]
![[Pasted image 20210401100008.png]]
if we add lable tag, if we click on lable name, the cursor automatically move to input field. #aha 



## navigating with tab index
![[Pasted image 20210401100241.png]]
tabindex attribute --> moves the cursor to input field in the given order.
this is to make the site more accessible for everyone.

# styling and validating
## applying styles to elements
![[Pasted image 20210401100738.png]]
![[Pasted image 20210401100754.png]]
this is the way we use css to apply to input fields.

## using css selectors
## validating form inputs from clients
![[Pasted image 20210401101055.png]]
but we also should validate on server side
we cant trust the client.
### validation attributes
![[Pasted image 20210401101215.png]]
required--> it'll make the field mandatory

## using styles to reflect validity
![[Pasted image 20210401101451.png]]
we can select the style depending on the validity of the input.
![[Pasted image 20210401101623.png]]

[[CSS styling]]