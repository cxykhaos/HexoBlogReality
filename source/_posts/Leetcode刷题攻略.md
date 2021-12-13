---
title: Leetcode刷题攻略
date: 2021-12-13 14:15:16
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.zhimg.com%2Fv2-3b79c3ad1b8398ba2afd440ee83ae32c_1440w.jpg%3Fsource%3D172ae18b&refer=http%3A%2F%2Fpic1.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1641738529&t=e45395cd290d520122676d409bf5acdf
categories: 
           - Leetcode
tags:
           - Leetcode
           - Java
---

:::tip Custom header

刷题注意

- 本文章自己平时leetcode的合集
- 仅供参考

:::

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.zhimg.com%2Fv2-3b79c3ad1b8398ba2afd440ee83ae32c_1440w.jpg%3Fsource%3D172ae18b&refer=http%3A%2F%2Fpic1.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1641738529&t=e45395cd290d520122676d409bf5acdf)

# 零、二分查找

## 简单模板

```java
class Solution{
    public void TFCZ(int nums[],int target){
    	int left=0,right=n-1;
    	while(left<right){
    		int mid = left+(right-left)/2; //向下取整
    		if(nums[mid]<target){ //向上取整则(l + r + 1)/2
        		left=mid+1;
    		}else{
        		right=mid;
        	}
    	}//最终返回的值是相同值的最左边。
    }
}
```

## 旋转后的数组中查找

```java
class Solution {
    public int search(int[] nums, int target) {
        int n = nums.length;
        if(n==0) return -1;
        if(n ==1) return nums[0]==target?0:-1;
        int left=0;
        int right=n-1;
        while(left<=right){
            int mid = left + (right-left)/2;
            if(nums[mid]==target) return mid;
            if(nums[0]>nums[mid]){
                if(target<=nums[n-1] && target>nums[mid]) left=mid+1;
                else right=mid-1;
            }
            else{
                if(target>=nums[0] && target<nums[mid]) right=mid-1;
                else left=mid+1;
            }
        }
        return -1;
    }
}
```



# 一、回溯

回溯如果不能重复可以加个visitd的boolean数组判断

```java
class Solution {
    List<String> 结果 = new ArrayList();
    public List<String> 结果函数(结果函数参数) {
        定义路径
        回溯(路径，选择列表);
        return 结果;
    }
    public void 回溯(路径，选择列表){
        if(满足结束条件) { 
            结果.add(路径);
            return ;
        }
        for(选择判断循环)
            做选择
            回溯(路径，选择列表);
            撤销选择
        }
    }
}
```



# 二、动态规划

```java
class Solution {
    public int numSquares(int n) {
     int []dp = new int[n+1];   
     for(int i=1;i<=n;i++){
         int Min = Integer.MAX_VALUE;
         for(int j=1;j*j<=i;j++){
             Min = Math.min(Min,dp[i-j*j]);
         }
         dp[i]=Min+1;
     }
     return dp[n];
    }
}
```







# 三、DFS



```java

```





# 四、BFS



```java
class Solution {
    public int[] BFS(TreeNode root) { //从上到下遍历二叉树
        if(root==null) return new int[0];
        Queue<TreeNode> queue = new LinkedList<>(){{ add(root);}};
        ArrayList<Integer> array = new ArrayList<Integer>();
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            array.add(node.val);
            if(node.left!=null) queue.add(node.left);
            if(node.right!=null) queue.add(node.right);
        }
        int[]res= new int[array.size()];
        for(int i=0;i<array.size();i++){
            res[i]=array.get(i);
        }
        return res;
    }
}
```





# 五、双指针



```java
/* 滑动窗口算法框架 */
void slidingWindow(string s, string t) {
    unordered_map<char, int> need, window;
    for (char c : t) need[c]++;

    int left = 0, right = 0;
    int valid = 0; 
    while (right < s.size()) {
        // c 是将移入窗口的字符
        char c = s[right];
        // 右移窗口
        right++;
        // 进行窗口内数据的一系列更新
        ...

        /*** debug 输出的位置 ***/
        printf("window: [%d, %d)\n", left, right);
        /********************/

        // 判断左侧窗口是否要收缩
        while (window needs shrink) {
            // d 是将移出窗口的字符
            char d = s[left];
            // 左移窗口
            left++;
            // 进行窗口内数据的一系列更新
            ...
        }
    }
}
```



# 六、贪心算法



```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int right = 0;
        for(int i=0;i<n;i++){
            if(i<=right){
                right = Math.max(right,i+nums[i]);
                if(right>=n-1) return true;
            }

        }
        return false;
    }
}
```



# 七、排序算法

## 快速排序

```java
public class main {
    public static int[] qsort(int arr[],int start,int end) {
        int p = arr[start];
        int i = start;
        int j = end;
        while(i<j){
            while((i<j)&&(arr[j]>p)){
                j--;
            }
            while((i<j)&&(arr[i]<p)){
                i++;
            }
            if(i<j && arr[i]==arr[j]){
                i++;
            }
            else{
                int t = arr[i];
                arr[i]=arr[j];
                arr[j]=t;
            }
            for (int t:arr) {
                System.out.print(t+"\t");
            }
            System.out.println();
        }
        if(i-1>start) arr = qsort(arr,start,i-1);
        if(j+1<end) arr = qsort(arr,j+1,end);
        return arr;
    }
    public static void main(String[] args) {
        int arr[] = new int[]{38,1,3,17,9,122,466,34,34,456,50,343,565,23,12321};
        int len = arr.length-1;
        for (int t:arr) {
            System.out.print(t+"\t");
        }
        System.out.println();
        arr=qsort(arr,0,len);
        for (int i:arr) {
            System.out.print(i+",");
        }
    }


}

```



# 八、链表

## 从尾到头打印链表

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> num = new ArrayList();
        ArrayList<Integer> res = new ArrayList();
        while(listNode!=null){
            num.add(listNode.val);
            listNode=listNode.next;
        }
		for(int i = num.size()-1;i>=0; i --){
            res.add(num.get(i));
        }
        
        return res;
    }
}
```



## 反转链表

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode ReverseList(ListNode head) {
        if(head==null) return null;
        ListNode pre = null;
        while(head!=null){
            ListNode next=head.next;
            head.next=pre;
            pre = head;
            head = next;
        }
        return pre;
    }
}
```



## 合并两个排序的链表

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        if(list1==null) return list2;
        if(list2==null) return list1;
        if(list1.val<=list2.val) {
            list1.next=Merge(list1.next,list2);
            return list1;}
        else {
            list2.next=Merge(list1,list2.next);  
            return list2;}
    }
}
```

## 两个链表的第一个公共结点

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
import java.util.HashSet;

public class Solution {
    public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {
        HashSet<ListNode> hashset = new HashSet<ListNode>();
        if(pHead1==null || pHead2==null) return null;
        while(pHead1!=null) {
            hashset.add(pHead1);
             pHead1= pHead1.next;
        }
        while(pHead2!=null){
            if(hashset.contains(pHead2)) return pHead2;
            pHead2= pHead2.next;
        }
        return null;
        
        
    }
}
```



## 链表中环的入口结点

```java
/*
 public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
*/
import java.util.*;
public class Solution {

    public ListNode EntryNodeOfLoop(ListNode pHead) {
        HashSet<ListNode> hashset = new HashSet();
        while(pHead!=null){
            if(hashset.contains(pHead)){
                return pHead;
            }
            hashset.add(pHead);
            pHead = pHead.next;
        }
        return null;
        
    }
}
```



## 链表中倒数最后k个结点

```java
    public ListNode FindKthToTail(ListNode pHead, int k) {
        if (pHead == null || k == 0) {
            return null;
        }
        int count = 0;
        ListNode temp = pHead;
        while (temp!=null) {
            count ++ ;
            temp = temp.next;
        }
        if (count < k) {
            return null;
        }
        temp = pHead;
        for (int i = 0; i < count - k; i++) {
            temp = temp.next;
        }
        return temp;
    }
```



## 复杂链表的复制

```java
/*
public class RandomListNode {
    int label;
    RandomListNode next = null;
    RandomListNode random = null;

    RandomListNode(int label) {
        this.label = label;
    }
}
*/
import java.util.*;
public class Solution {
        Map<RandomListNode, RandomListNode> cachedNode = new HashMap<RandomListNode, RandomListNode>();
        public RandomListNode Clone(RandomListNode pHead) {
         if (pHead == null)   return null;
        if (!cachedNode.containsKey(pHead)) {
            RandomListNode headNew = new RandomListNode(pHead.label);
            cachedNode.put(pHead, headNew);
            headNew.next = Clone(pHead.next);
            headNew.random = Clone(pHead.random);
        }
        return cachedNode.get(pHead); 
    }
}
```



## 删除链表中重复的结点

```java
public class Solution {
    public ListNode deleteDuplication(ListNode pHead) {
        if (pHead == null || pHead.next == null) { // 只有0个或1个结点，则返回
            return pHead;
        }
        if (pHead.val == pHead.next.val) { // 当前结点是重复结点
            ListNode pNode = pHead.next;
            while (pNode != null && pNode.val == pHead.val) {
                // 跳过值与当前结点相同的全部结点,找到第一个与当前结点不同的结点
                pNode = pNode.next;
            }
            return deleteDuplication(pNode); // 从第一个与当前结点不同的结点开始递归
        } else { // 当前结点不是重复结点
            pHead.next = deleteDuplication(pHead.next); // 保留当前结点，从下一个结点开始递归
            return pHead;
        }
    }
}
```





# 九、二叉树

## 二叉树的深度

```java
public class Solution {
    public int TreeDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        return Math.max(TreeDepth(root.left),TreeDepth(root.right))+1;
        
    }
}
```

## 按之字形顺序打印二叉树

```java
import java.util.ArrayList;
/*
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
import java.util.*;
public class Solution {
    public ArrayList<ArrayList<Integer> > Print(TreeNode pRoot) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if(pRoot==null) return res;
        Deque<TreeNode>deque = new LinkedList();
        deque.push(pRoot);
        int level = 0;
        while(!deque.isEmpty()){
            ArrayList<Integer> array = new ArrayList();
            int size = deque.size();
            while(size-->0){
                TreeNode cur = deque.pop();
                if(level%2==0){
                    array.add(cur.val);
                }else{
                    array.add(0,cur.val);
                }
                if(cur.left!=null){
                    deque.addLast(cur.left);
                }
                if(cur.right!=null){
                    deque.addLast(cur.right);
                }
            }
           level++;
           res.add(array);
        }
        
        return res;
    }

}
```

## 二叉搜索树的第k个结点

```java
import java.util.*;
public class Solution {
    TreeNode KthNode(TreeNode pRoot, int k) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = pRoot;
        while(!stack.isEmpty() || cur!=null){
            while(cur!=null){
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            if(k==1)
                return cur;
            k--;
            cur = cur.right;
        }
        return null;
    }
}
```



## 重建二叉树

### 方法一：

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
import java.util.*;
public class Solution {
    HashMap<Integer,Integer> hashmap = new HashMap();
    int []pre;
    public TreeNode reConstructBinaryTree(int [] pre,int [] vin) {
        this.pre = pre;
        for(int i =0 ;i<vin.length;i++){
            hashmap.put(vin[i],i);
        }
        return recur(0,0,pre.length-1);
    }
    public TreeNode recur(int root , int left, int right){
        if(left>right ) return null ;
        TreeNode node = new TreeNode(pre[root]);
        int cur = hashmap.get(pre[root]);
        node.left=recur(root+1,left,cur-1);
        node.right=recur(root+1+cur-left,cur+1,right);
        
        return node;
    }
    
}
```



### 方法二：

```java
class Solution {
    Map<Integer,Integer> hashmap= new HashMap();
    int []pre;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = inorder.length;
        this.pre = preorder;
        for(int i =0;i<n;i++) hashmap.put(inorder[i],i);
        return recur(0,n-1,0,n-1);
    }
    public TreeNode recur(int pre_left,int pre_right,int ino_left,int ino_right){
        if(pre_left>pre_right) return null;
        int pre_root = pre_left;
        int ino_root = hashmap.get(pre[pre_root]);
        TreeNode root = new TreeNode(pre[pre_root]);
        int size=ino_root-ino_left;
        root.left =recur (pre_root+1,pre_root+size,ino_left,ino_root-1);
        root.right=recur (pre_root+size+1,pre_right,ino_root+1,ino_right);
        return root;
    }

}
```



## 树的子结构

```java

```



## 二叉树的镜像

```java

```



## 从上往下打印二叉树

```java

```



## 二叉搜索树的后序遍历序列

```java

```



## 二叉树中和为某一值的路径

```java

```



## 二叉搜索树与双向链表

```java

```



## 平衡二叉树

```java

```



## 二叉树的下一个结点

```java

```



## 对称的二叉树

```java

```



## 把二叉树打印成多行

```java

```



## 序列化二叉树

```java

```









# 十、图





# 十一、哈希表



```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head){
        HashSet<ListNode> set = new HashSet();
        while(head!=null) {
            if(set.contains(head)){
                return head;
            }           
            set.add(head);
            head = head.next;
        }
        return null;
    }
}
```

