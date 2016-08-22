# LeetCodee 9. Palindrome Number
##題目
Determine whether an integer is a palindrome. Do this without extra space.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

##翻譯
判斷一個int整數是否是自己的迴文數，不能使用額外的空間來操作。  
  
提示：  
負整數會是自己的迴文數嗎(ex. -1)  
  
如果你想用字串來解是不行的，因為不能使用額外的空間。  
   
你也可以反轉整數，如果你之前已經做過[LeetCode 7. Reverse Integer](questions/7md.md)，你會知道反轉後的數可能會超過integer的最大值。

##思路
不使用額外空間的意思，根據discuss裡面的討論，應該是不能用一個O(n)的額外空間(ex. array, string之類的)，用一個O(1)的變數是可以的。
把傳入的x整個反轉後跟本來的x比較是否一致，這題還算簡單，直接看code。
  
##解題
```
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    // x < 0 or x > (2^32 - 1) , false;
    if(x < 0 || x > Math.pow(2,32)-1) return false;
    if(x < 10) return true;
    
    // keep x
    var num = x;
    
    // 先抓出最高位數，轉成個位數
    var recNum = x%10;
    x  = parseInt(x/10);
    
    // 將recNum*10，再抓最高位數加到recNumb
    while(x != 0){
        recNum = recNum*10;
        recNum = recNum + x%10;
        x = parseInt(x/10);
    }
    return recNum == num;
};
```
