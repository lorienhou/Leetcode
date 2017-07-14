Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

Note:
The order of the result is not important. So in the above example, [5, 3] is also correct.
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?
```java
public class Solution {
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for(int n : nums){
        	xor = n^xor;
        }
        //now xor=a^b, find the first bit that's 1, a and b must differ on this bit
        int i=0;
        while(( (xor>>i & 1) != 1) && i<32)
        	i++;
        //split array into 2 subarrays, one with a, the other with b -> becomes 2 SingleNumberI problems
        xor = 0;
        int xor2 = 0;
        for(int n : nums){
        	if((n>>i & 1)==1){
        		xor = n^xor;
        	}else{
        		xor2 = n^xor2;
        	}
        }
        int[] result = new int[2];
        result[0] = xor;
        result[1] = xor2;
        return result;
    }
}
```
