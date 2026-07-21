
url: https://youtu.be/5rtVTYAk9KQ

#todo 

- [ ] Converting Binary to decimal and vice versa


# AND
result is true if all operands are true.
result is false if any of the operand is false.

- [ ] finding N is even or odd?
	- % operator is expensive
	- `if(n&1 == 0)` -> this is fast
- [ ] check if i th bit set or not
	- AND with `(1<<i)` Check if answer is 0 or 1
	- `(1<<i)` is called mask

- [ ] extract the i th bit of number
	- AND with `(1<<i)` Check if answer is 0 or 1
- [ ] clear the i th bit
	- `number & ~(1<<i)` AND with negation of mask.
	- ![[Pasted image 20220619045854.png]]
- [ ] Remove the last set bit
	- `n&(n-1)`
- [ ] check if number is power of 2
	- if `n&(n-1)==0`
- [ ] count the number of set bits
	- increment count until `n=n&(n-1)` becomes 0.
	- ```
    
```cpp
int count_one (int n)
        {
            while( n )
            {
            n = n&(n-1);
               count++;
            }
            return count;
    }
```
- [ ] creating subsets
	- ![[Pasted image 20220619053523.png]]
```cpp
void possibleSubsets(char A[], int N)
    {
        for(int i = 0;i < (1 << N); ++i)
        {
            for(int j = 0;j < N;++j)
                if(i & (1 << j))
                    cout << A[j] << ‘ ‘;
            cout << endl;
    }
    }
```


# OR
result is true if any of the operand is 1.

## **Find the largest power of 2 [(most significant bit](https://en.wikipedia.org/wiki/Most_significant_bit) in binary form), which is less than or equal to the given number N.**
```cpp
long largest_power(long N)
    {
        //changing all right side bits to 1.
        N = N| (N>>1);
        N = N| (N>>2);
        N = N| (N>>4);
        N = N| (N>>8);


    //as now the number is 2 * x-1, where x is required answer, so adding 1 and dividing it by
     2. 
                return (N+1)>>1;

    }
```

# XOR
if there are even number of true values,  result is false.

- [ ] finding the number in array which is repreated only once/odd times(given that we have only one such number in array)
- [ ] swap two numbers using XOR
	- ![[Pasted image 20220619043951.png]]
- [ ] find XOR of all numbers from 1 to N #doubt
	- dont use loop as it'll be O(N)
	- ![[Pasted image 20220619044412.png]]
- [ ] Finding XOR between Numbers L and R
	- ![[Pasted image 20220619044816.png]]
- [ ] xor of all subsets of array, th results will always be 0.
- [ ]  

# Negation
it flips the bits.

# Right shift
`>>` will move all bits to the right.
right shift by x bit, it'll divide the number by 2^x .


# Left Shift
`<<` wil move bits to the left.
left shift by x bit, it'll multiply the number by 2^x.

Remember integers are 32 bits.
overflow will happen in left shift and we'll get negative numbers.




