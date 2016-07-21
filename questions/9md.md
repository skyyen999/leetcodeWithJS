# LeetCodee 9. Palindrome Number
##題目
Determine whether an integer is a palindrome. Do this without extra space.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

##翻譯
判斷一個int整數是否是自己的迴文數，不能使用額外的空間來操作

提示：  
負整數會是自己的迴文數嗎(ex. -1)
  
如果你想用字串來解是不行的，因為不能使用額外的空間。
  
你也可以反轉整數，如果你之前已經做過"Reverse Integer"，你會知道反轉後的數可能會超過integer的最大值。

##思路
1. 
##解題
```
/**
 * @param {number} n
 * @return {number}
 */
var trailingZeroes = function(n) {
    if(n < 5) return 0 ;
    
    var count = 0;
    // 算階層內有幾個5出現
    while(n >= 5){
        count += Math.floor(n/5);
        n = parseInt(n/5);
    }

    return count;
};
```
