# LeetCode 2. Add Two Numbers

##題目
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order  
and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

##翻譯
有兩個連結陣列分別代表兩個非負整數，他們的位數是反向儲存(越前面的節點位數越低)，毎一個節點代表一個位數，將這兩個連結陣列加總後以連結陣列形式回傳。

範例：  
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)  
Output: 個位數為2與5，相加為7 ； 十位數為4+6 = 10，需要進位 ； 百位數為3 + 4 + 1(進位) = 8，結果為 7->0->8  
  
##思路
1. 就只是用一個新的linked list來儲存相加後的結果
2. 要注意的就是list1跟list2長度可能不一樣
3. 另外就是相加後可能比9還大，需要考慮進位的情況
  
##解題
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var list = new ListNode(0); //儲存輸出的結果，因為list的指針要不斷往後移，因此用一個假節點方便操作
    var result = list; // 使用一個ListNode來儲存相加的結果

    var sum,carry = 0; // carry用來處理進位
    
	//當 list1, list2 都沒有值，而且carry也為0的時候才結束迴圈
    while(l1 || l2 || carry > 0){
        sum = 0;
		
		// list1與list2長度可能不同，分開處理
        if(l1!== null){
            sum += l1.val;
            l1 = l1.next;
        }
        
        if(l2!==null){
            sum += l2.val;
            l2 = l2.next;
        }
		
		// 如果之前有進位，carry = 1；沒有的話carry = 0
        sum += carry;
        list.next = new ListNode(sum%10); //相加如果超過9，只能留下個位數放入結果list，十位數的地方進位
        carry = parseInt(sum/10);
        
		// list指標向後
		list = list.next;
    }
	// 因為第一個節點為假節點，跳過
    return result.next;
}	
```

##用遞迴解
```
var addTwoNumbers = function(l1, l2) {
  
    var list = new ListNode(0);
    var result = list; // 使用一個ListNode來儲存相加的結果
   
    add(l1,l2,0);
    return result.next;
    
    function add(l1,l2,gap){
        var sum = 0;
        if(l1 === null && l2 === null && gap === 0){
            return 0;
        } 
        
        if(l1 !== null){
            sum += l1.val;
            l1 = l1.next;
        } 
        
        if(l2 !== null){
            sum += l2.val;
            l2 = l2.next;
        }
        sum += gap;
        list.next = new ListNode(sum%10);
        gap = parseInt(sum/10);
        list = list.next;
        add(l1,l2,gap);
    }
};
```