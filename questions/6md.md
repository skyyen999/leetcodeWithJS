# LeetCode 6. ZigZag Conversion

##題目
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
<pre>
P   A   H   N
A P L S I I G
Y   I   R
</pre>

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

<pre>
string convert(string text, int nRows);
</pre>

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".  
  
##翻譯
字串"PAYPALISHIRING"經過Z字轉換後如圖所示，重組後變成"PAHNAPLSIIGYIR"，
寫一個convert(string text, int nRows)來將傳入的字串text轉換成n行的Z字轉換
  
convert("PAYPALISHIRING", 3) 會回傳 "PAHNAPLSIIGYIR".

這邊用另外一個範例來解釋會比較清楚：  
text = "ABCDEFGHIJKLMN", n = 4，排成Z字如下，因此轉換後的字串為 "AGMBFHLNCEIKDJ"
<pre>
A     G     M
B   F H   L N
C E   I K   
D     J     
</pre>


##思路
1. 從上面nRows=3，nRows=4觀察可以知道，字母要回到第一列總共要經過 2*nRows - 2次變化，例如上面的例子A->G之間總共經過 2*4-2 = 6個字母
2. 用一個array來儲存毎一列的字母，上面範例最後array[0] = 'AGM'
3. n = 2*nRows - 2代表實際上經過的字母數，字母位置為i， i%n < nRows時，直接將字母放入array[i]，  
   例如"B"的位置i為1，1%6 = 1， 將"B"放入array[1]
4. 當i%n >= nRows時， 放入的位置為 nRows-1 - (i%n) - nRows -1，整理一下可以寫成2*nRows - i%n - 2  
   例如上面的"F" [i=5, i%6 = 5], 5 > 4 因此"F"在array中的位置為 2*4 - 5 - 2 = 1，  
   因此將"F"放到array[1]，也就是array[1] = "BF"
5. 最後將array內的字串結合回傳   
  
##解題
```
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    if(s == null) return "";
    if(numRows == 1)  return s;
    
    // 毎一輪的變化總共是numRows*2 - 2種
    var n = numRows*2 - 2;
    var array = [];
    
    // 創立一個有numRows元素的array
    for(var k = 0 ; k < numRows; k++){
        array.push("");
    }

    for(var i in s){
        var lineNumber = i%n;
        if(lineNumber < numRows){
            // i%n 比 numRows小，s[i]直接放入array
            array[lineNumber] += s[i]; 
        } else {
            // 計算s[i]應該屬於array哪個位子
            //array[numRows-1 - lineNumber-numRows-1] += s[i]; 
            array[2*numRows - lineNumber -2] += s[i]; 
        }
    }
    
    return array.join("");
};
```
