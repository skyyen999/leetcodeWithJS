# LeetCode 8. String to Integer (atoi)

##題目
Implement atoi to convert a string to an integer.  
  
Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.  
  
Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.  

Requirements for atoi:  
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.  
  
The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.  
  
If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.  
  
If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.  
  
##翻譯
實作atoi將字串轉成int。  
  
提示：小心仔細的考慮所有可能的輸入，如果你想挑戰自己，不要看下面的文字，直接想可能的輸入有哪些就可以開始寫了。
  
注意：這題目的輸入值有各種組合，你要先收集任何可能的輸入。  
  
atoi的需求：  
首先輸入的開頭可能是一連串的空白，因此要先找到第一個非空白字元。然後從這個字元開始可能會有正負號在數字的前面，將這些字串轉換成數字。  
    
如果在數字後面有出現其他非數字的符號，因為他們對值沒有影響，可以忽略這些符號。  
  
如果第一個非空白字元不是一個合法的int整數，或者字串裡面都是空白字元，那也視為不合法的輸入。  
  
不合法的輸入回傳0，如果轉換後的數字num > INT_MAX (2147483647) 回傳2147483647， num <  INT_MIN (-2147483648) 回傳 -2147483648  
     
##思路
這題看起來很複雜，通過率也低的很可怕，莫驚莫怕莫慌張，其實慢慢的一邊改一邊做，經過大量的Trial & Error，為拉低通過率做出一點貢獻，最後還是解得出來。  
  
這邊當然不是來說一句Trial & Error，這題可以拆成以下幾個步驟一步一步解開：  
1. 先把字串前面可能出現的空白字串都消除，找到第一個出現得+-符號或數字。  
  
2. 如果剩下的開頭是+-符號，先用一個變數存放起來，然後把他截掉。  
  
3. 如果輸入的字串是合法的，理論上現在開頭就應該只剩下數字，如果又出現+-號或其他字元，就可以判定為不合法字串。 
  
4. 經過上面3取到最後都是數字，不過這沒影響。關，剩下的開頭肯定是數字了，這代表我們一定可以解析出一個整數出來，接下來將開頭到不是數字字元中間的數字字串取出來，當然也有可能一直到最後都是數字，不過這沒影響。  
  
5. 結合剛才儲存的正負符號與上一個步驟拿到的數字字串後轉換成整數，這時候還要判斷整數是否超過int的最大值(2147483647)與最小值(-2147483648)，超過的話上面題目已經說明過要怎麼處理，沒超過就直接回傳解析後的整數。

##解題
```
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function(str) {
    var sign = '+'; //正負號
    var numReg = /^[0-9]/;
    
    //將前面的空白字串去掉,  ex. "^^^^-122a" -> "-122a" (^代表空白) 
    var i = 0;
    while(str.charAt(i)==' ' && i < str.length){
        i++;
    }
    str = str.slice(i);
 
    
    //處理正負號, ex. "-122a" -> "122a"
    if(str.startsWith('+')){
        str = str.slice(1);
    } else if(str.startsWith('-')){
        str = str.slice(1);
        sign = '-';
    }
    
    //處理後的字串不是數字開頭,代表字串不合法 
    if(!numReg.test(str)) return 0;

    //出現不是數字的符號就中斷
    var j = 0;
    while(j < str.length && numReg.test(str[j])){
        j++;
    };
    // 截出開頭的數字字串, ex. '122a' -> '122'
    str = str.substr(0,j);

    //字串轉成int
    var value = parseInt(sign+str);
    if(value > 2147483647){
        return 2147483647;
    }
    if(value < -2147483648){
        return -2147483648;
    }   
    return value;
};
```
