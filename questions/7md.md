# LeetCode 7. Reverse Integer

##題目
Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

##翻譯
反轉一個int整數

提示：  
負整數會是自己的迴文數嗎(ex. -1)
  
如果你想用字串來解是不行的，因為不能使用額外的空間。
  
你也可以反轉整數，如果你之前已經做過"Reverse Integer"，你會知道反轉後的數可能會超過integer的最大值。

##思路
1. 
##解題
```
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    var INT_MAX = Math.pow(2,31)-1;    
    if(0 <= x && x < 10) return x;
    
    var nFlag = "";
    // x to string
    var str = x.toString();
    // if start with '-', cut and save it
    if(str.charAt(0) == '-'){
        str = str.replace('-','');
        nFlag = '-';
    } 
    
    
    // reverse number string
    var rStr = nFlag + str.split("").reverse().join("");
    var result = parseInt(rStr);
    
    if(result > INT_MAX || result < -(1+INT_MAX)) return 0;
    return result;
};
```
