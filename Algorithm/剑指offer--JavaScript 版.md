## 剑指 offer

1. 在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```js
function Find(target, array){
    var rowCount = array.length - 1, i, j;

    for(i=rowCount,j=0; i >= 0 && j < array[i].length;){
        if(target == array[i][j]){
            return true;
        }else if(target > array[i][j]){
            j++;
            continue;
        }else if(target < array[i][j]){
            i--;
            continue;
        }
    }
    return false;
}
```

2. 请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

```js
function replaceSpace(str){
    return str.replace(/ /g, '%20');
}
```

3. 输入一个链表，从尾到头打印链表每个节点的值。

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function printListFromTailToHead(head){
    if(!head){
        return 0;
    } else {
        var arr = new Array();
        var curr = head;
        while(curr){
            arr.push(curr.val);
            curr = curr.next;
        }
        return arr.reverse();
    }
}
```

4. 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function reConstructBinaryTree(pre, vin){
    if(pre.length == 0 || vin.length == 0){
        return null;
    };
    var index = vin.indexOf(pre[0]);
    var left = vin.slice(0,index);
    var right = vin.slice(index+1);
    var node = new TreeNode(vin[index]);
    node.left = reConstructBinaryTree(pre.slice(1,index+1),left);
    node.right = reConstructBinaryTree(pre.slice(index+1),right);
    return node;
}
```

5. 用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

```js
var stack1 = [];
var stack2 = [];

function push(node){
    stack1.push(node);
}

function pop(){
    var temp = stack1.pop();
    while(temp){
        stack2.push(temp);
        temp = stack1.pop();
    }
    var result = stack2.pop();
    temp = stack2.pop();
    while(temp){
        stack1.push(temp);
        temp = stack2.pop();
    }
    return result;
}
```

6. 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

```js
function minNumberInRotateArray(rotateArray){
    var len = rotateArray.length;
    if(len === 0){
        return 0;
    }
    return Math.min.apply(null,rotateArray);
}
```

7. 大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。n<=39

```js
function Fibonacci(n){
    var a = 1, b = 1, temp;
    if(n <= 0) return 0;
    for(var i = 2; i <= n; i++){
      temp = b;
      b = a + b;
      a = temp;
    }
    return a;
}
```

8. 一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```js
function jumpFloor(number){
    if(number < 1){
        return 0;
    }
    if(number === 1){
        return 1;
    }
    if(number === 2){
        return 2;
    }
    var temp = 0, a = 1, b = 2;
    for(var i = 3; i <= number; i++){
        temp = a + b;
        a = b;
        b = temp;
    }
    return temp;
}
```

9. 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
```js
function jumpFloorII(number){
  return Math.pow(2, number - 1);
}
```
10. 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

```js
function rectCover(number){
    var a = 1, b = 2, temp;
    if(number <= 0){
        return 0;
    }
    if(number === 1){
        return 1;
    }
    if(number === 2){
        return 2
    }
    for(var i = 3; i <= number; i++){
      temp = a + b;
      a = b;
      b = temp;
    }
    return temp;
}
```

11. 输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

```js
function NumberOf1(n){
    if(n < 0){
        n = n >>> 0;
    }
    var arr = n.toString(2).split('');
    return arr.reduce(function(a,b){
        return b === "1" ? a + 1 : a;
    },0);
}
```

12. 给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

```js
function Power(base, exponent){
    return Math.pow(base, exponent);
}
```

13. 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

```js
function reOrderArray(array){
    var result = [];
    var even = [];
    array.forEach(function(item){
        if((item & 1) === 1){
            result.push(item);
        } else {
            even.push(item);
        }
    });
    return result.concat(even);
}
```

14. 输入一个链表，输出该链表中倒数第k个结点。

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindKthToTail(head, k){
    if(!head || k <= 0){
        return null;
    }
    var i = head, j = head;
    while(--k){
        j = j.next;
        if(!j){
            return null;
        }
    }
    while(j.next){
        i = i.next;
        j = j.next;
    }
    j = null;
    return i;
}
```

15. 输入一个链表，反转链表后，输出链表的所有元素。

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function ReverseList(pHead){
    var newHead, temp;
    if(!pHead){
        return null;
    }
    if(pHead.next === null){
        return pHead;
    } else {
        newHead = ReverseList(pHead.next);
    }
    temp = pHead.next;
    temp.next = pHead;
    pHead.next = null;
    temp = null;
    return newHead;
}
```

16. 输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function Merge(pHead1, pHead2){
    if(!pHead1){
        return pHead2 ? pHead2 : null
    } else if(!pHead2){
        return pHead1;
    }
    // debugger;
    var curr1 = pHead1;
    var curr2 = pHead2;
    var result = new ListNode(-1);
    var curr = result;
    while(curr1 && curr2){
        if(curr1.val < curr2.val){
            curr.next = curr1;
            curr1 = curr1.next;
        } else{
            curr.next = curr2;
            curr2 = curr2.next;
        }
        curr = curr.next;
    }
    if(curr1){
        curr.next = curr1;
    }
    if(curr2){
        curr.next = curr2;
    }

    //防止内存泄露
    curr = result.next;
    result.next = null;
    result = curr;
    curr = curr1 = curr2 = null;

    return result;
}
```

17. 输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

```js
function HasSubtree(pRoot1, pRoot2){
    if(pRoot1 == null || pRoot2 == null){
        return false;
    }
    if(isSubTree(pRoot1, pRoot2)){
        return true;
    } else{
        return HasSubtree(pRoot1.left, pRoot2) || HasSubtree(pRoot1.right, pRoot2);
    }

    function isSubTree(pRoot1, pRoot2){
        if(pRoot2 == null) return true;
        if(pRoot1 == null) return false;
        if(pRoot1.val === pRoot2.val){
            return isSubTree(pRoot1.left, pRoot2.left) && isSubTree(pRoot1.right, pRoot2.right);
        } else {
            return false;
        }

    }
}
```

18. 操作给定的二叉树，将其变换为源二叉树的镜像。

```js
function Mirror(root){
    if(!root){
        return null;
    }
    var temp = root.left;
    root.left = root.right;
    root.right = temp;
    if(root.left){
        Mirror(root.left);
    }
    if(root.right){
        Mirror(root.right);
    }
}
```

19. 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

```js
function printMatrix(matrix){
    if(!matrix || !matrix.length) return null;
    var result = [];
    var rows = matrix.length, cols = matrix[0].length;
    var len = rows * cols;
    var i = 0, j = 0;
    var circle = 0;
    while(1){
        while(j < cols - circle){
            result.push(matrix[i][j]);
            j++;
        }
        if(result.length === len) break;
        j--, i++;
        while(i < rows - circle){
            result.push(matrix[i][j])
            i++;
        }
        if(result.length === len) break;
        i--, j--;
        while(j >= circle){
            result.push(matrix[i][j]);
            j--;
        }
        if(result.length === len) break;
        j++, i--;
        circle++;
        while(i >= circle){
            result.push(matrix[i][j])
            i--;
        }
        if(result.length === len) break;
        j++, i++;
    }
    return result;
}
```

20. 定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。

```js
var stack = [];
function push(node){
    stack.push(node);
}
function pop(){
    return stack.pop();
}
function top(){
    return stack[stack.length - 1];
}
function min(){
    return Math.min.apply(null, stack);
}
```

21. 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4，5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

```js
function IsPopOrder(pushV, popV){
    if(!pushV.length || !popV.length){
        return false;
    }
    var temp = [];
    var popIndex = 0;
    var len = pushV.length;
    for(var i = 0; i < len; i++){
        temp.push(pushV[i]);
        while(temp.length && temp[temp.length - 1] === popV[popIndex]){
            temp.pop();
            popIndex++;
        }
    }
    return temp.length === 0;
}
```

22. 从上往下打印出二叉树的每个节点，同层节点从左至右打印。

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function PrintFromTopToBottom(root){
    if (!root) {
        return [];
    }
    var queue = [];
    queue.push(root);
    var result = [];

    while (queue.length) {
        var temp = queue.shift();
        result.push(temp.val);
        if (temp.left) {
            queue.push(temp.left);
        }
        if (temp.right) {
            queue.push(temp.right);
        }
    }
    return result;
}
```

23. 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。(测试用例用的是 false/true, 不是题目中的 'Yes'/'No')

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function VerifySquenceOfBST(sequence) {
    var len = sequence.length
    if (!len) {
        return false;
    }
    return adjustSequence(0, len - 1);

    function adjustSequence(start, end){
        if (start >= end) {
            return true;
        }
        var root = sequence[end];
        for(var i = start; i < end && sequence[i] < root; i++);
        var index = i;
        for (i = i + 1; i < end; i++) {
            if (sequence[i] < root) {
                return false;
            }
        }
        return adjustSequence(start, index - 1) && (adjustSequence(index, end - 1));
    }
}
```

24. 输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function FindPath(root, expectNumber){
    var temp = [];
    // var found = false;
    var result = [];
    dfs(root, 0);
    return result;
    function dfs(root, sum){
      // debugger;s
        if(!root){
            return;
        }
        temp.push(root.val);
        sum += root.val;
        if(!root.left && !root.right && sum === expectNumber){
            result.push(temp.concat());
        }
        if(root.left){
            dfs(root.left, sum);
        }
        if(root.right){
            dfs(root.right, sum);
        }
        temp.pop();
        return;
    }
}
```

25. 输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

```js
function Clone(pHead)
{
    if(!pHead){
        return null;
    }
    var head = new RandomListNode(pHead.label);
    head.random = pHead.random;
    head.next = Clone(pHead.next);
    return head;
}
```

26. 输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

> 将左子树构成双向链表，返回的是左子树的尾结点，将其连接到root的左边；
> 将右子树构成双向链表，将其追加到root结点之后，并返回尾结点；
> 向左遍历返回的链表至头结点处，即为所求双向链表的首结点。

```js
function Convert(pRootOfTree){
    if(!pRootOfTree) {
        return null;
    }
    var lastNode = null;
    lastNode = ConvertNode(pRootOfTree);
    var head = lastNode;
    while(head && head.left) {
        head = head.left;
    }
    return head;

    function ConvertNode(node){
        if(!node){
            return;
        }
        if(node.left) {
            lastNode = ConvertNode(node.left);
        }
        node.left = lastNode;
        if(lastNode){
            lastNode.right = node;
        }
        lastNode = node;
        if(node.right){
            lastNode = ConvertNode(node.right);
        }
        return lastNode;
    }
}
```

27. 输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

```js
function Permutation(str){
    if(!str || str.length === 0){
        return [];
    }
    var result = [];
    var arr = str.split('');
    var temp = '';
    ordering(arr);
    result = result.filter(function(item, index){  //去重
      return result.indexOf(item) === index;
    });
    return result;

    function ordering(tempArr){
        if(tempArr.length === 0){
            result.push(temp);
            return;
        }
        for(var i = 0; i < tempArr.length; i++){
            temp += tempArr[i];
            insideArr = tempArr.concat();
            insideArr.splice(i,1);
            ordering(insideArr);
            temp = temp.substring(0, temp.length - 1);   //回溯
        }
    }
}
```

28. 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

```js
function MoreThanHalfNum_Solution(numbers){
    if(!numbers || numbers.length === 0){
        return 0;
    }
    var arr = [];
    var len = numbers.length, index;
    for(var i = 0; i < len; i++){
      var index = numbers[i];
      arr[index] !== undefined ? arr[index]++ : arr[index] = 1;
    }
    var index = -1;
    var arrLen = arr.length;
    var max = -Infinity;
    for(var i = 0; i < arrLen; i++){
      if(!arr[i]) continue;
      max = arr[i] > max ? (index = i, arr[i]) : max;
    }
    return max > len / 2 ? index : 0;
}
```

29. 输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。

```js
function GetLeastNumbers_Solution(input, k){
    if(!input || input.length < k){
        return [];
    }
    return input.sort(function(a,b){
        return a - b
    }).slice(0, k);
}
```

30. HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。你会不会被他忽悠住？(子向量的长度至少是1)

```js
function FindGreatestSumOfSubArray(array){
    if (array.length < 0)
        return 0;
    var sum = array[0],
        tempsum = array[0];
    for (var i = 1; i < array.length; i++) {
        tempsum = tempsum < 0 ? array[i] : tempsum + array[i];
        sum = tempsum > sum ? tempsum : sum;
    }
    return sum;
}
```

31. 求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数。

```js
function NumberOf1Between1AndN_Solution(n)
{
    if (n < 0) return 0;
    var ones = 0;
    var arr = [];
    while(n){
        arr.push(n);
        n--;
    }
    return arr.join('').replace(/[^1]+/g,'').length;
}
```

32. 输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

```js
function PrintMinNumber(numbers)
{
    if(!numbers || numbers.length === 0){
        return [];
    }
    var result = [];
    var temp = '';
    ordering(numbers);

    result = result.map(Number).reduce(function(min , a){  //最小值
      return min < a ? min : a;
    }, Infinity);
    return result;

    function ordering(tempArr){
        var innerLen = 0;
        if(tempArr.length === 0){
            result.push(temp);
            return;
        }
        for(var i = 0; i < tempArr.length; i++){
            innerLen = tempArr[i].toString().length;
            temp += tempArr[i];
            insideArr = tempArr.concat();
            insideArr.splice(i,1);
            ordering(insideArr);
            temp = temp.substring(0, temp.length - innerLen);   //回溯
        }
    }
}
```

33. 把只包含因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

```js
function GetUglyNumber_Solution(index) {
    if (index === 0) return 0;
    var uglyNum = [1];
    var factor2 = 0, factor3 = 0, factor5 = 0;
    for (var i = 1; i < index; i++) {
        uglyNum[i] = Math.min(uglyNum[factor2] * 2, uglyNum[factor3] * 3, uglyNum[factor5] * 5);
        if (uglyNum[i] === uglyNum[factor2] * 2) factor2++;
        if (uglyNum[i] === uglyNum[factor3] * 3) factor3++;
        if (uglyNum[i] === uglyNum[factor5] * 5) factor5++;
    }
    return uglyNum[index - 1];
}
```

34. 在一个字符串(1<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置

```js
function FirstNotRepeatingChar(str){
    if(!str || !str.length){
        return -1;
    }

    var hash = {};
    var tempArr = str.split('');
    var unique = [];
    var len = str.length, temp;
    for(var i = 0; i < len; i++){
        temp = tempArr[i];
        if(hash[temp]){
            hash[temp].push(i);
        } else {
            hash[temp] = [i];
        }
    }
    for(var key in hash){
        if(hash.hasOwnProperty(key)){
            if(hash[key].length === 1){
                unique.push(hash[key].pop());
            }
        }
    }

    return Math.min.apply(null, unique);

}
```

35. 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

> 由于时间空间复杂度的限制，js 貌似无法完成这个题，所以使用 c++ 完成。

```cpp
class Solution {
public:
    long long InversePairsCore(vector<int> &data, vector<int>&copy, int start, int end){
        if(start == end){
            copy[start] = data[start];
            return 0;
        }
        int length = (end - start) / 2;
        long long left = InversePairsCore(copy, data, start, start + length);
        long long right = InversePairsCore(copy, data, start + length + 1, end);

        int i = start + length;
        int j = end;
        int indexCopy = end;
        long long count=0;
        while(i >= start && j >= start + length + 1){
            if(data[i] > data[j]){
                copy[indexCopy--] = data[i--];
                count += j - start - length;
            } else {
                copy[indexCopy--] = data[j--];
            }
        }
        for(; i >= start; --i)
            copy[indexCopy--] = data[i];
        for(;j >= start + length + 1; --j)
            copy[indexCopy--] = data[j];
        return left + right + count;
    }
    int InversePairs(vector<int> data) {
        int length = data.size();
        if(length <= 0)
            return 0;
        vector<int> copy;
        for(int i = 0; i < length; i++)
            copy.push_back(data[i]);
        long long count = InversePairsCore(data, copy, 0, length-1);
        copy.clear();
        return count % 1000000007;
    }
};
```

36. 输入两个链表，找出它们的第一个公共结点。

```js
function FindFirstCommonNode(pHead1, pHead2){
    if(!pHead1 || !pHead2){
        return null;
    }
    var len1 = getLength(pHead1);
    var len2 = getLength(pHead2);
    var lenDiff = len1 - len2;

    var curr1 = pHead1;
    var curr2 = pHead2;
    if(len2 > len1){
        curr1 = pHead2;
        curr2 = pHead1;
        lenDiff = len2 - len1;
    }

    for(var i = 0; i < lenDiff; ++i)
        curr1 = curr1.next;

    while(curr1 && curr2 && curr1 != curr2){
        curr1 = curr1.next;
        curr2 = curr2.next;
    }

    return curr1;

    function getLength(node){
        var len = 0;
        curr = node;
        while(curr){
            len++;
            curr = curr.next;
        }
        return len;
    }
}
```

37. 统计一个数字在排序数组中出现的次数。

```js
function GetNumberOfK(data, k){
    return data.reduce(function(count, a){
        return a === k ? count+1 :count;
    }, 0);
}
```

38. 输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

```js
function TreeDepth(pRoot){
    if(!pRoot){
        return 0;
    }

    var depth = 0;
    var currDepth = 0;
    dfs(pRoot);
    return depth;

    function dfs(node){
        if(!node){
            depth = depth > currDepth ? depth : currDepth;
            return;
        }
        currDepth++;
        dfs(node.left);
        dfs(node.right);
        currDepth--;
    }
}
```

39. 输入一棵二叉树，判断该二叉树是否是平衡二叉树。

```js
function IsBalanced_Solution(pRoot){
    if(!pRoot){
        return true;
    }

    var left = TreeDepth(pRoot.left);
    var right = TreeDepth(pRoot.right);
    var diff = left - right;

    if(diff > 1 || diff < -1)
        return false;

    return IsBalanced_Solution(pRoot.left) && IsBalanced_Solution(pRoot.right);

    function TreeDepth(pRoot){
        if(!pRoot){
            return 0;
        }

        var depth = 0;
        var currDepth = 0;
        dfs(pRoot);
        return depth;

        function dfs(node){
            if(!node){
                depth = depth > currDepth ? depth : currDepth;
                return;
            }
            currDepth++;
            dfs(node.left);
            dfs(node.right);
            currDepth--;
        }
    }
}
```

40. 一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

```js
function FindNumsAppearOnce(array){
    if (!array || array.length < 2)
        return [];
    return array.sort().join(',').replace(/(\d+),\1/g,"").replace(/,+/g,',').replace(/^,|,$/, '').split(',').map(Number);
}
```

41. 小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

```js
function FindContinuousSequence(sum){
    if(sum < 3){
        return [];
    }
    var small = 1, big = 2;
    var mid = (1 + sum) / 2;
    var curr = small + big;
    var result = [];

    while(small < mid){
        if(curr === sum){
            pushSeq(small, big);
        }
        while(curr > sum && small < mid){
            curr -= small;
            small++;
            if(curr === sum){
                pushSeq(small, big);
            }
        }
        big++;
        curr += big;
    }

    result.sort(function(a,b){return a[0] - b[0];});
    return result;

    function pushSeq(small, big){
        var temp = [];
        for(var i = small; i <= big; i++){
            temp.push(i);
        }
        result.push(temp);
    }
}
```

42. 输入一个递增排序的数组和一个数字S，在数组中查找两个数，是的他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

```js
function FindNumbersWithSum(array, sum){
    if(!array || !array.length){
        return [];
    }
    var result = [];
    var product = [];
    var head = 0, tail = array.length - 1;
    while(head < tail){
        var curr = array[head] + array[tail];
        if(curr === sum){
            result.push([array[head], array[tail]]);
            product.push(array[head] * array[tail]);
            tail--;
            head++;
        } else if(curr > sum){
            tail--;
        } else {
            head++;
        }
    }
    if(result.length === 0){
        return [];
    }
    var min = Math.min.apply(null, product);
    var index = product.indexOf(min);
    return result[index];
}
```

43. 汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

```js
function LeftRotateString(str, n){
    if(!str){
        return "";
    }
    var len = str.length;
    n = n % len;
    var left = str.slice(0,n);
    var right = str.slice(n);
    return right + left;
}
```

44. 牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

```js
function ReverseSentence(str){
    return str.split(' ').reverse().join(' ');
}
```

45. LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何。为了方便起见,你可以认为大小王是0。

```js
function IsContinuous(numbers){
    if(!numbers || numbers.length < 1){
        return false;
    }
    var len = numbers.length;
    numbers.sort(function(a,b){return a - b;});

    var zeros = 0, gaps = 0;
    for(var i = 0; i < len && numbers[i] == 0; i++){
        zeros++;
    }
    var small = zeros, big = small + 1;
    while(big < len){
        if(numbers[small] == numbers[big]){
            return false;
        }
        gaps += numbers[big] - numbers[small] - 1;
        small = big++;
    }
    return gaps <= zeros;
}
```

46. 每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

```js
function LastRemaining_Solution(n, m){
    if(n < 1 || m < 1){
        return -1;
    }
    var last = 0;
    for(var i = 2; i <= n; i++){
        last = (last + m) % i;
    }
    return last;
}
```

47. 求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

```js
function Sum_Solution(n){
  var sum = 0;
  plus(n);
  return sum;

  function plus(num){
    sum += num;
    num > 0 && plus(--num);
  }
}
```

48. 写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。

```js
function Add(num1, num2){
    var sum, carry;
    do{
        sum = num1 ^ num2;
        carry = (num1 & num2) << 1;
        num1 = sum;
        num2 = carry;
    }while(num2 != 0);
    return num1;
}
```

49. 将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0

```js
function StrToInt(str){
    if(str.length === 0){
        return 0;
    }
    var format = str.match(/^(\+?|-?)(\d+)$/);
    if(!format){
        return 0;
    }
    var num = 0;
    var temp = format[2];
    var base = 1;
    var flag = format[1];
    for(var i = temp.length - 1; i >= 0; i--){
        num += parseInt(temp[i]) * base;
        base *= 10;
    }

    return flag === '-' ? num * (-1) : num;
}
```

50. 在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

```js
function duplicate(numbers, duplication){
    if(!numbers || !numbers.length){
        return false;
    }
    var len = numbers.length;
    for(var i = 0; i < len; i++){
        var curr = numbers[i];
        if(numbers.indexOf(curr) !== i){
            duplication[0] = curr;
            return true;
        }
    }
    return false;
}
```

51. 给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

```js
function multiply(array){
    if(!array || !array.length){
        return [];
    }
    var result = [];
    var len1 = array.length, len2 = result.length;
    result[0] = 1;
    for(var i = 1; i < len1; i++){
        result[i] = array[i - 1] * result[i - 1];
    }
    var temp = 1;
    for(var i = len1 - 2; i >= 0;--i){
        temp *=array[i + 1];
        result[i] *= temp
    }
    return result;
}
```

52. 请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配

```js
function match(s, pattern)
{
    if(s === "" && pattern === ""){
        return true;
    }
    if(!pattern || pattern.length === 0){
        return false
    }
    var reg = new RegExp('^' + pattern + '$');
    return reg.test(s);
}
```

53. 请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

```js
function isNumeric(s){
    var reg = /^[+-]?(?:(\d+)(\.\d+)?|(\.\d+))([eE][+-]?\d+)?$/;
    return reg.test(s);
}
```

54. 请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

```js
function Init(){
    streamNums = [];   //定义一个全局变量, 不用var
    streamNumsLen = 256;   //定义一个全局变量, 不用var
    streamNumsIndex = 0;   //定义一个全局变量, 不用var

    for(var i = 0; i < streamNumsLen; i++){
        streamNums[i] = -1;
    }
}

function Insert(ch){
    var code = ch.charCodeAt();
    if(streamNums[code] == -1){
        streamNums[code] = streamNumsIndex;
    } else if(streamNums[code] >= 0){
        streamNums[code] = -2;
    }
    streamNumsIndex++;
}

function FirstAppearingOnce(){
    result = '';
    var ch = '';
    var minIndex = Infinity;
    for(var i = 0; i < streamNumsLen; i++){
        if(streamNums[i] >= 0 && streamNums[i] < minIndex){
            ch = String.fromCharCode(i);
            minIndex = streamNums[i];
        }
    }
    return ch == "" ? '#' : ch;
}
```

55. 一个链表中包含环，请找出该链表的环的入口结点。

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function EntryNodeOfLoop(pHead){
    if(!pHead){
        return null;
    }
    var meeting = meetingNode(pHead);
    if(!meeting){
        return null;
    }
    var nodeLoop = 1;
    var node1 = meeting;
    while(node1.next != meeting){
        node1 = node1.next;
        nodeLoop++;
    }
    node1 = pHead;
    for(var i = 0; i < nodeLoop; i++){
        node1 = node1.next;
    }
    var node2 = pHead;
    while(node1 != node2){
        node1 = node1.next;
        node2 = node2.next;
    }
    return node1;

    function meetingNode(node){
        if(!node || !node.next){
            return null;
        }
        var slow = node.next;
        var fast = slow.next;

        while(fast && slow){
            if(fast === slow){
                return fast;
            }
            slow = slow.next;
            fast = fast.next;
            if(fast){
                fast = fast.next;
            }
        }
        return null;
    }
}
```

56. 在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

```js
function deleteDuplication(pHead){
    if(!pHead){
        return null;
    }
    var tempHead = new ListNode(-1);
    tempHead.next = pHead;
    var preNode = tempHead;
    var curr1 = preNode.next;
    var curr2 = curr1.next;

    while(curr1){
        if(!curr2 || curr2.val !== curr1.val){
            if(curr1.next !== curr2){
                clear(curr1, curr2);
                preNode.next = curr2;
            } else {
              preNode = curr1;
            }

            curr1 = curr2;
            if(curr2){
              curr2 = curr2.next;
            }
        } else {
          if(curr2){
            curr2 = curr2.next;
          }
        }
    }
    return tempHead.next;

    function clear(node, stop){
        var temp;
        while(node !== stop){
            temp = node.next;
            node.next = null;
            node = temp;
        }
    }
}
```

57. 给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

```js
function GetNext(pNode){
    if (!pNode){
        return pNode;
    }
    if (pNode.right){
        pNode = pNode.right;
        while (pNode.left) {
            pNode = pNode.left;
        }
        return pNode;
    } else if(pNode.next && pNode.next.left == pNode){
        return pNode.next;
    } else if(pNode.next && pNode.next.right == pNode){
        while(pNode.next && pNode.next.left != pNode){
            pNode = pNode.next ;
        }
        return pNode.next;
    } else {
        return pNode.next;
    }
}
```

58. 请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

```js
function isSymmetrical(pRoot){
    if(!pRoot){
      return true;
    }
    return symmetrical(pRoot, pRoot);

    function symmetrical(node1,node2){
        if(!node1 && !node2)
            return true;
        if(!node1 || !node2)
            return false;
        if(node1.val != node2.val)
            return false;
        return symmetrical(node1.left, node2.right) && symmetrical(node1.right, node2.left);
    }
}
```

59. 请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

```js
function Print(pRoot) {
    var res = [];
    if(!pRoot){
        return res;
    }
    var que = [];
    que.push(pRoot);
    var flag = false;
    while(que.length > 0){
        var vec = [];
        var len = que.length;
        for(var i = 0; i < len; i++){
            var tmp = que.shift(); //front
            vec.push(tmp.val);
            if(tmp.left)
                que.push(tmp.left);
            if(tmp.right)
                que.push(tmp.right);
        }
        if(flag){
            vec.reverse();
        }
        res.push(vec);
        flag = !flag;
    }
    return res;
}
```

60. 从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

```js
function Print(pRoot) {
    var res = [];
    if(!pRoot){
        return res;
    }
    var que = [];
    que.push(pRoot);
    while(que.length > 0){
        var vec = [];
        var len = que.length;
        for(var i = 0; i < len; i++){
            var tmp = que.shift(); //front
            vec.push(tmp.val);
            if(tmp.left)
                que.push(tmp.left);
            if(tmp.right)
                que.push(tmp.right);
        }
        res.push(vec);
    }
    return res;
}
```

61. 请实现两个函数，分别用来序列化和反序列化二叉树

```js
function Serialize(pNode) {
    var str = [];
    ser(pNode);

    for(var i = str.length - 1; i >= 0; i--){
      if(str[i] !== '#'){
        break;
      }
      str.pop();
    }

    return str.join();

    function ser(node){
        if(!node){
            str.push('#');
            return;
        }
        str.push(node.val);
        ser(node.left);
        ser(node.right);
    }
}
function Deserialize(str) {
    var index = -1;
    var len = str.length;
    if(index >= len){
        return null;
    }
    var arr = str.split(",");
    var head = des();

    return head;

    function des(node){
        index++;
        if(arr[index] && arr[index] !== '#'){
            var temp = new TreeNode(arr[index]);
            node = temp;
            node.left = des();
            node.right = des();
        }
        return node;
    }
}
```

62. 给定一颗二叉搜索树，请找出其中的第k大的结点。例如， 5 / \ 3 7 /\ /\ 2 4 6 8 中，按结点数值大小顺序第三个结点的值为4。

```js
function KthNode(pRoot, k){
    if(!pRoot || !k){
        return null;
    }
    return KthCore(pRoot);

    function KthCore(node){
        var target = null;

        if(node.left){
            target = KthCore(node.left);
        }
        if(!target){
            if(k === 1)
                target = node;
            k--;
        }

        if(!target && node.right)
            target = KthCore(node.right);

        return target;
    }
}
```

63. 如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

```js
var arr = [];
function Insert(num){
    arr.push(num);
    arr.sort(function(a,b){
        return a - b;
    });
    return arr;
}
function GetMedian(){
    var mid = Math.floor(arr.length / 2);
    if((arr.length & 1) === 0){
        var n1 = arr[mid];
        var n2 = arr[mid - 1];
        return (n1 + n2) / 2;
    } else {
        return arr[mid]
    }
}
```

64. 给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

```js
function maxInWindows(num, size){
    if(!num || num.length === 0){
        return null;
    }
    var max = [];
    if(num.length >= size && size >= 1){
        var index = [];

        for(var i = 0; i < size; ++i){
            while(index.length > 0 && num[i] >= num[index[index.length - 1]])
                index.pop();
            index.push(i);
        }

        for(var i = size; i < num.length; ++i){
            max.push(num[index[0]]);
            while(index.length > 0 && num[i] >= num[index[index.length - 1]])
                index.pop();
            if(index.length > 0 && index[0] <= i - size)
                index.shift();
            index.push(i);
        }
        max.push(num[index[0]]);
    }
    return max;
}
```

65. 请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如 a b c e s f c s a d e e 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

```js
function hasPath(matrix, rows, cols, path){
    var visited = [];
    for(var i = 0; i < rows * cols; i++){
        visited[i] = false;
    }
    var pathLen = 0;
    try{
        for(var i = 0; i < rows; i++){
            for(var j = 0; j < cols; j++){
                if(core(i,j)){
                    return true;
                }
            }
        }
    } finally {
        visited.length = 0;
    }

    return false;

    function core(row, col){
        if(path.length === pathLen){
            return true;
        }
        var hasPath = false;
        if(row >= 0 && row < rows && col >= 0 && col < cols && matrix[row * cols + col] === path[pathLen] && !visited[row * cols + col]){
            pathLen++;
            visited[row * cols + col] = true;
            hasPath = core(row - 1, col)+ core(row, col - 1)
                    + core(row + 1, col) + core(row, col + 1);
            if(!hasPath){
                pathLen--;
                visited[row * cols + col] = false;
            }
        }
        return hasPath;
    }
}
```

66. 地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

```js
function movingCount(threshold, rows, cols){
    var visited = [];
    for(var i = 0; i < rows * cols; ++i)
        visited[i] = false;
    var count = movingCountCore(0, 0);
    visited.length = 0;
    return count;

    function getDigitSum(number){
        var sum = 0;
        while(number > 0){
            sum += number % 10;
            number = Math.floor(number / 10);
        }
        return sum;
    }

    function check(row, col){
        if(row >= 0 && row < rows && col >= 0 && col < cols && getDigitSum(row) + getDigitSum(col) <= threshold && !visited[row * cols + col])
            return true;
        return false;
    }

    function movingCountCore(row, col){
        var count = 0;
        if(check(row, col)) {
            visited[row * cols + col] = true;
            count = 1 + movingCountCore(row - 1, col)
                    + movingCountCore(row, col - 1)
                    + movingCountCore(row + 1, col)
                    + movingCountCore(row, col + 1);
        }
        return count;
    }
}
```

## 手动测试框架

- 二叉树构造
```js
function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
}
function Tree(arr, node, num = 1){
    if(!arr || arr.length === 0){
        return new TreeNode(null);
    }
    node = node || new TreeNode(arr[num - 1]);
    var curr = node;
    if(num * 2 - 1 < arr.length && arr[num * 2 - 1]){
      curr.left = new TreeNode(arr[num * 2 - 1]);
      Tree(arr, curr.left, num * 2);
    }
    if(num * 2 < arr.length && arr[num * 2]){
      curr.right = new TreeNode(arr[num * 2]);
      Tree(arr, curr.right, num * 2 + 1);
    }
    return node;
}
// 根据数组生成二叉树
var tree = new Tree([3,2,4,8,7,null,10,null,null,5,9]);
console.log(tree);
```

- 单向链表构造
```js
function ListNode(x){
    this.val = x;
    this.next = null;
}
function LinkedList(arr){
    if(!arr || arr.length === 0){
        return new ListNode(null);
    }
    var head = new ListNode(arr[0]);
    var len = arr.length;
    var curr = head;
    for(var i = 1; i < len; i++){
        var temp = new ListNode(arr[i]);
        curr.next = temp;
        curr = curr.next;
    }
    return head;
}
var ll = new LinkedList([3,2,4,8,7,10,5,9]);
console.log(ll);
```

- 牛客网 Node.js 多行输入测试 (如果不能运行请更新浏览器来支持 es6 语法)
```js
(function(){

  /* Todo: This Array contains the input lines in sequence. Each of the elements is like a line of input. */
  var test_lines =['5','1 2 3 3 5','3','1 2 1','2 4 5','3 5 3'];   // Do not change the name of this array if you don't like bugs.

  /****************************************************************
  Todo: Add your code here including the callback function of event 'rl.on()' and
  global variables except the statements and definitions of 'readline' and 'rl'.
  *****************************************************************/

  /* global variables here */
  var lines = 1;

  /* callback function of 'rl.on()' */
  function main(line) {    // Do not change the name of this function if you don't like bugs.
    var str = line.trim();
    console.log('lines',lines++,':',str);
  }

  /**************** End of Your Code *****************/

  (function(){
    var test_len = test_lines.length;
    var test_it = gen(test_lines);
    var test_val = test_it.next();
    while(test_len){
       main(test_val.value);
       test_val = test_it.next();
       test_len--;
     }
    function* gen(test_lines){
      var len = test_lines.length;
      var i = 0;
      while(len){
        yield test_lines[i];
        i++;
      }
    }
  }())
}());
```
