# LeetCodee 9. Palindrome Number
Determine whether an integer is a palindrome. Do this without extra space.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

##題目
判斷一個int整數是否是自己的迴文數，不能使用額外的空間來操作

提示：  
負整數會是自己的迴文數嗎(ex. -1)
  
如果你想用字串來解是不行的，因為不能使用額外的空間。
  
你也可以反轉整數，如果你之前已經做過"Reverse Integer"，你會知道反轉後的字數能 
##翻譯
給一個正整數n，回傳n!中有幾個0

注意：你的解法應該是logN的時間複雜度

範例：
n = 5 ; n! = 120 回傳 1  
    
##思路
1. 要出現0，也就是10的n次方，可以推論一定要出現2跟5
2. 2這個數字到處撿都是，所以真正決定會出現幾個0的，是n!裡面包含幾個5
3. 例如上面的n=5，5*4*3*2*1 = 120，可以發現5*2 =10，因此會出現一個0
4. n = 25，會出現 25,20,15,10,5共5個帶有5的數字，不過25其實包含了5*5，所以25!總共會出現5+1=6個10。

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
