# this need to be optimized using dictionary
```cs
using System;
//[2,3,7] - target 9 ,  [3,3,0] -> target 6 .
// 0,2  ;; 0,1
					
public class Program
{
	public static void Main()
	{
		int target = 9;
		int[] arr = [2,3,7];
		//int flag1 = arr[0];
		//int flag2 = arr[1];
		for(int i = 0; i< arr.Length - 1; i++){
			for(int j = i+1; j<arr.Length - 2; j++){
				if(arr[i]+arr[j] == target){
					Console.WriteLine(i);
					Console.WriteLine(j);
				}
			}
		}
	}
}*/
```