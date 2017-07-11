Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.


Example 1:

Input: k = 3, n = 7

Output:

[[1,2,4]]
```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(k<=0 || n<k || n>9*k)
            return result;
        find(1, k, n, new ArrayList<Integer>(), result);
        return result;
    }
    private void find(int start, int k, int remain, List<Integer> list, List<List<Integer>> result){
        if(remain==0 && k==0){
            result.add(new ArrayList<Integer>(list));
            return;
        }
        if(k<=0 || remain<=0 || start>9 || remain<start)
            return;
        list.add(start);
        find(start+1, k-1, remain-start, list, result);
        list.remove(list.size()-1);
        find(start+1, k, remain, list, result);
    }
}
```
