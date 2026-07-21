Given that a device:
	Takes a reading every 5 minutes
	May have a unique combination of sensors that are included in the readings
	Attempts to send a combined reading file (mainData) every 15 minutes
	Will continue appending readings onto the mainData file until it is received
 
Given that ingestion:
	Sends an ack back to controller after receiving the file
	Gets necessary information about the controller (an IoT device) from the mainData filename
	Does not open the mainData file
 
We need to display to users how many mainData files are received on time in a given month 

---

Problem: Given an array of a variable number of integers, find the two numbers that add up to a specific target number.
 
	Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]

	Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
	
	
int target = 9;
int[] nums = [2, 7, 11, 15];

dictionary<int, int> pairs = new dictionary<int, int>();

for(int i=0; i<nums.Length; i++){
	pairs[i] = target - nums[i];
	if(pairs.ContainsKey(nums[i]){
		Console.WriteLine(
	}
}

for(int i=0; i<nums.Length; i++){
	for(int j=i; j<nums.Length - i; j++){
		if(nums[i] + nums[j] == target){
			Console.WriteLine(i, j);
		}
	}
}

Input: nums = [2, 7, 6, 11, 3, 15], target = 9
Output: [0,1], [2,4]