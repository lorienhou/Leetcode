Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.

Thoughts: maintain 3 queues, starting with 2,3,5. Each time i'm taking the smallest head among the queues and add to the result list.
However, if at least one queue is empty, i'm going to take a number from result list in order, then multiply by 2,3,5 respectively and add them to tails of the queues.
Then I advance the pointer of the last taken number in the result list.
```java
public class Solution {
    public int nthUglyNumber(int n) {
        int[] pos = new int[3];//denotes which ugly number each row already multipled
        int[] nums = new int[n];
        nums[0] = 1;
        Arrays.fill(pos, 0);
        int i = 1;
        while (i < n) {
            int next2 = nums[pos[0]] * 2;
            int next3 = nums[pos[1]] * 3;
            int next5 = nums[pos[2]] * 5;
            if (next2 <= next3 && next2 <= next5) {
                if (nums[i-1] != next2) 
                    nums[i] = next2;
                else
                    i--;
                pos[0]++;
            } else if (next3 <= next2 && next3 <= next5) {
                if (nums[i-1] != next3)
                    nums[i] = next3;
                else
                    i--;
                pos[1]++;
            } else {
                if (nums[i-1] != next5)
                    nums[i] = next5;
                else
                	i--;
                pos[2]++;
            }
            i++;
        }
        return nums[n-1];
    }
}
```
