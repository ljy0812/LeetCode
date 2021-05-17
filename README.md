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


3)


Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:

Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
Example 2:

Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
 

Constraints:

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums is sorted in non-decreasing order.

```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) 
    {
        vector<int> sortedVec;
        for(auto num : nums)
        {
            sortedVec.push_back(num*num);
        }
        sort(sortedVec.begin(), sortedVec.end());
        return sortedVec;
    }
};
```

```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) 
    {
        int cnt = 0;
        
        for(const auto& num : nums)
        {
            nums[cnt] = num*num;
            cnt++;
        }
        quickSort(nums, 0, cnt-1);
        
        return nums;
    }
    
    void quickSort(vector<int>& nums, int start, int end)
    {
        if(start >= end)
        {
            return;
        }
        
        int i = start-1;
        int j = start;
        int& pivot = nums[end];
        for(; j<end; ++j)
        {
            if(nums[j] < pivot)
            {
                swap(nums[++i], nums[j]);
            }
        }
        swap(nums[++i], pivot);
        
        quickSort(nums, start, i-1);
        quickSort(nums, i+1, end);       
    }
    
    void swap(int &a, int &b)
    {
        int t = a; 
        a = b; 
        b = t;
    }

};
```


210503

1)
Given a fixed length array arr of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written.

Do the above modifications to the input array in place, do not return anything from your function.

 

Example 1:

Input: [1,0,2,3,0,4,5,0]
Output: null
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]
Example 2:

Input: [1,2,3]
Output: null
Explanation: After calling your function, the input array is modified to: [1,2,3]
 
 
```
class Solution {
public:
    void duplicateZeros(vector<int>& arr) {
                
        for(int i=0; i<arr.size(); ++i)
        {
            if(arr[i] == 0)
            {                
                for(int j=arr.size()-1; j>i; --j)
                {
                    arr[j] = arr[j-1];
                }
                ++i;
            }
        }
    }
};
```

```
class Solution {
public:
    void duplicateZeros(vector<int>& arr) {
                
        for(int i=0; i<arr.size(); ++i)
        {
            if(arr[i] == 0)
            {                
                arr.insert(arr.begin()+i, 0);
                arr.pop_back();
                ++i;
            }
        }
    }
};
```


2)
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]
 

Constraints:

2 <= nums.length <= 103
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        int i;
        int j;
        
        for(i = 0; i<nums.size(); ++i)
        {
            for(j=i+1; j<nums.size(); ++j)
            {
                if((nums[i]+nums[j]) == target)
                {
                    result.push_back(i);
                    result.push_back(j);
                    return result;
                }
            }
            
        }
        return result;
    }
};
```


210511

1)

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

The number of elements initialized in nums1 and nums2 are m and n respectively. You may assume that nums1 has a size equal to m + n such that it has enough space to hold additional elements from nums2.

 

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
 

Constraints:

nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-109 <= nums1[i], nums2[i] <= 109
 

Follow up: Can you come up with an algorithm that runs in O(m + n) time?

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        
        if(n == 0)
        {
            return;
        }
        
        if(m == 0)
        {
            for(int i = 0; i < n; ++i)
            {
                nums1.insert(nums1.begin() + i, nums2[i]);
                nums1.pop_back();
            }
            return;
        }

        int insertIndex = n-1;
        for(int i = m; i > 0; --i)
        {
            if(nums1[i-1] < nums2[insertIndex])
            {
                nums1.insert(nums1.begin() + i, nums2[insertIndex]);
                nums1.pop_back();
                --insertIndex;
                ++i;
                if(insertIndex < 0)
                {
                    break;
                }
            }
        }
        for(int i = 0; i <= insertIndex; ++i)
        {
            nums1.insert(nums1.begin() + i, nums2[i]);
            nums1.pop_back();
        }
    }
};
```

210517

1) Remove Element
Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means a modification to the input array will be known to the caller as well.

Internally you can think of this:

// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
 

Example 1:

Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 2.
It doesn't matter what you leave beyond the returned length. For example if you return 2 with nums = [2,2,3,3] or nums = [2,2,0,0], your answer will be accepted.
Example 2:

Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3]
Explanation: Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4. Note that the order of those five elements can be arbitrary. It doesn't matter what values are set beyond the returned length.


```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {

        vector<int>::iterator it;
        for(it=nums.begin(); it!=nums.end(); ++it)
        {
            if(val == *it)
            {
                nums.erase(it);
                it--;
            }
        }
        return nums.size();
    }
};
```

```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int i = 0;
        for (int j = 0; j < nums.size(); j++) 
        {
            if (nums[j] != val) 
            {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
};
```

