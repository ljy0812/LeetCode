# LeetCode
Daily LeetCode

210428

1)

Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
Example 2:

Input: nums = [1,0,1,1,0,1]
Output: 2
 

Constraints:

1 <= nums.length <= 105
nums[i] is either 0 or 1.




```
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int maxNumOfConsecutiveOnes = 0;
        int currentNumOfConsecutiveOnes = 0;
        
        for(const auto& num : nums)
        {
            if(num == 1)
            {
                currentNumOfConsecutiveOnes++;
                 
                if(currentNumOfConsecutiveOnes > maxNumOfConsecutiveOnes)
                {
                    maxNumOfConsecutiveOnes = currentNumOfConsecutiveOnes;
                }
            }
            else
            {
                currentNumOfConsecutiveOnes = 0; 
            }
        }
        return maxNumOfConsecutiveOnes;
    }
};
```

2)

Given an array nums of integers, return how many of them contain an even number of digits.

Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 
12 contains 2 digits (even number of digits). 
345 contains 3 digits (odd number of digits). 
2 contains 1 digit (odd number of digits). 
6 contains 1 digit (odd number of digits). 
7896 contains 4 digits (even number of digits). 
Therefore only 12 and 7896 contain an even number of digits.
Example 2:

Input: nums = [555,901,482,1771]
Output: 1 
Explanation: 
Only 1771 contains an even number of digits.
 

Constraints:

1 <= nums.length <= 500
1 <= nums[i] <= 10^5

```
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int countOfEvenNumOfDigits = 0;
        int numOfDigits = 0;
        int currNum = 0;
        
        for(const auto& num : nums)
        {
            numOfDigits = 0;
            currNum = num;
            
            while(currNum != 0)
            {
                currNum = currNum/10;
                numOfDigits++;
            }
            if(numOfDigits%2 == 0)
            {
                countOfEvenNumOfDigits++;
            }
            
        }
        return countOfEvenNumOfDigits;
    }
};
```


```
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int countOfEvenNumOfDigits = 0;
        
        for(const auto& num : nums) {
            if(std::to_string(num).size() % 2 == 0) {
                countOfEvenNumOfDigits++;
            }
        }
        return countOfEvenNumOfDigits;
    }
};
```
