# LeetCode 1. Two Sum

##題目
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
<pre>
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
</pre>

##翻譯
給一個裡面元素為int的陣列，陣列中會有兩個元素加起來等於target，回傳這兩個元素的位置
  
範例：
[2, 7, 11, 15], target = 9，2+7=9，因此回傳[1,2]
  
##思路
1. 使用雙迴圈，如果nums[i]+nums[j] = target 就回傳i,j
  
##解題
```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    
    var map = {};
    for(var i = 0 ; i < nums.length ; i++){
        var v = nums[i];

        for(var j = i+1 ; j < nums.length ; j++ ){
            if(  nums[i] + nums[j]  == target ){
                return [i,j];
            }
        }
  
    }
};
```
  
#進階  
上面雙迴圈的時間複雜度是O(n^2)，效率明顯不太好，用map就可以在一次走訪中找到i,j的位置
```
var twoSum = function(nums, target) {
    
    var map = {};
    for(var i = 0 ; i < nums.length ; i++){
        var v = nums[i];
        
        if(map[target-v] >= 0){
            // 如果 target - v可以在map中找到值x，代表之前已經出現過值x， target = x + v
            // 因此回傳 x的位置與目前v的位置  
            return [map[target-v],i]
        } else {
            // 使用map儲存目前的數字與其位置  
              
			map[v] = i;
        }
    }
};
```