---
alias: [query, pkm, knowledge management, ]
Status: 
Medium: youtube1 
Tags: [obsidian, data, pkm]
url: https://youtu.be/sEgzrRNkgsE
---
___
# dataview tutorial

1. Broad Intro to Dataview
2. Metadata
3. Dataview Queries
	- List
	- F rom
	- Where
	- Task
	- Table
	- Sort
	- Flatten
	-  Group by

Treat your obsidian vault as a database which you can query from. Provides a fully-fledged query language for filtering,
sorting, and extracting data from your pages.

What is Metadata?
Metadata provides information about your data.
It is extra info that is either already inherent in your
data, or info that you manually add.
example:
Photographs
	• Date & time
	• Location
	• People



Markdown Notes
We can also add metadata to Markdown notes using
a language called YAMI.
• YAML is a structured way of adding arbitrary
metadata to a file.


Adding YAML Metadata
1. At the top of your note, add 3 dashes `---`
2. Underneath that, you can start adding key-value
pairs in the form
key: value
• In the photo example, this would look as follows:
![[Pasted image 20221221035424.png]]
3. To finish the metadata block, close it off with 3
dashes again.

## YAML Lists
You can add more than one value 
to each key
using
value
key
lists.
There are two notations you can use:
1. INLINE

![[Pasted image 20221221035500.png]]
2. Indented
	1. ![[Pasted image 20221221035628.png]]

make sure u space instead of tabs.


![[Pasted image 20221221035638.png]]


![[Pasted image 20221221035727.png]]

![[Pasted image 20221221035759.png]]

# List
```sql
list 
```

![[Pasted image 20221221040333.png]]
![[Pasted image 20221221040348.png]]
![[Pasted image 20221221040354.png]]
![[Pasted image 20221221040410.png]]
![[Pasted image 20221221040432.png]]


![[Pasted image 20221221040514.png]]
![[Pasted image 20221221040604.png]]
AND 
OR
Negation


![[Pasted image 20221221040649.png]]
![[Pasted image 20221221040718.png]]
![[Pasted image 20221221040813.png]]


After choosing which notes to use, you can narrow down the list further using a `where`
block.



![[Pasted image 20221221041835.png]]
![[Pasted image 20221221042128.png]]

![[Pasted image 20221221042150.png]]

![[Pasted image 20221221042630.png]]

![[Pasted image 20221221042653.png]]

![[Pasted image 20221221042701.png]]


```dataview
Table url, medium
where medium

```

