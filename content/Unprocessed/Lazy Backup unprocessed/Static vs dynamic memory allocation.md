Static vs dynamic memory allocation.

here we are size of main memory of 64KB.
65536 = 0 to 65535 = 64KBytes

in reality, the memory is divided into segments.

![[Pasted image 20210927090944.png]]

here we are assuming int takes 2 bytes. float as 4 bytes. in reality, space consumed will depend on compiler.


stack frame
activation record --> this is where static memory allocation happens.

memory allocation done during **compile time** is called **static memory allocation**.

how memory allocated insde stacks for sequence of function calls?

first machine code in code section.
for every fuction call/exection, there'll be section of stack allocated.

![[Pasted image 20210927091741.png]]

stack memory is automatically allocated and automatcally destroyed.
>the way stack memory is utilized is on the basis of LISO (like a stack) -> hence the name `stack`
>last activation record is executed first and removed from the stack before moving on to the next activation record.





Dynamic allocation:

heap word can be used for both organized and unorganized .

here in DSA, it is unorganized.

it should be treated as resource (external device)
and while not using, release it. (just like any other external resource)



it should be accessed from the pointer.

pointer takes the size of interger.

lets consider 2 bytes.

![[Pasted image 20210927092034.png]]

when we dont need the memory, we should deallocated.

![[Pasted image 20220624094236.png]]

so, explicitly requested and explicitly released.

if we forget to deallocate, this'll lead to loss of memory available -> this is called memory leakage.

if the not deallocated, this memory may become full 
