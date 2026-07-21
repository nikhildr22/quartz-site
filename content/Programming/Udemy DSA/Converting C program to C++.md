Class and Constructors:

```cpp
Class Rectangle
{
private:
	int length;
	int breadth;
	
public:
	Rectangle(int l, int b)
	{
		length = l;
		breadth = b;
	}
	
	int area()
	{
		return length*breadth;
	}
	
	void changeLength(int l)
	{
		length =  l;
	}
}

int main()
{
	Rectangle r = new Rectangle(10,6);
	
	//Rectangle r(10,6);
	r.area();
	r.changeLength(12);
	
	return 0;

}
```

