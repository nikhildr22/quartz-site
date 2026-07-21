---
alias: []
Status: 
Medium: 
Tags: 
url: https://youtu.be/XaES2G3PVpg
---
___
# Obsidian Plugin Dev

![[Pasted image 20220812044012.png]]
![[Pasted image 20220812044331.png]]
--> use this template

clone the repo you generated.

main.ts mail code
manifest.json obsidian meta
style.css for css styling.

Then do npm install to get all required packages.


![[Pasted image 20220812045115.png]]
--> this is very important  class for the plugin.

![[Pasted image 20220812045155.png]]
--> this method gets excecuted everytime plugin loads.

![[Pasted image 20220812045251.png]]
--> these are settings configurations

==Note that obsidian cant execute typescript, we need Ts to be compiled to js==

![[Pasted image 20220812045451.png]]
we'll use `npm run build` command to compile ts.

![[Pasted image 20220812045608.png]]
--> create a new folder in your obsidian workspace path.

![[Pasted image 20220812045637.png]]
--> paste these 3 files after compiling ts to js.

note that the compiled js will not be human readable (atleast hard to read)


reload the app for the first time.
from next time, we just need to reload the plugin when we make new changes.

![[Pasted image 20220812051019.png]]
--> lets start from scratch

add whatever logic you like.

then test.

These we've to edit the manifest.json before publishing the plugin.


Push your changes to git.
Create  a release.
![[Pasted image 20220812052435.png]]
![[Pasted image 20220812052447.png]]
create new release

![[Pasted image 20220812052525.png]]
add the final build files.

If you want to add it to community plugins list?
![[Pasted image 20220812052625.png]]
edit this file and make a pull request.
No need to clone, from github, edit this file and make a pull request.

Code reviews will happen and community will review.

This'll take few days.




