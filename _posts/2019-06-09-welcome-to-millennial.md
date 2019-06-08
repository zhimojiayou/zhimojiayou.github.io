---
layout: post
title: "ARTS_Week1!"
author: "zhimojiayou"
categories: documentation
tags: [documentation,sample]
image: cuba-1.jpg
---

# 算法
  暂时用的力扣中国<br>
  1.[反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)<br></br>
  ```
  class Solution {
      public ListNode reverseList(ListNode head) {
          ListNode pre = null;
          ListNode curr = head;
          while (curr != null) {
              ListNode temp = curr.next;
              curr.next = pre;
              pre = curr;
              curr = temp;
          }
          return pre;
      }
  }
  ```
  主要在于定义前后两个引用，需要通过画图来清晰自己的思维，开始的时候光凭想，便开始写
  代码，容易被弄晕。<br>
  
  2.[两数相加](https://leetcode-cn.com/problems/add-two-numbers/)
   ``` 
   class Solution {
       public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
           ListNode head = null;
           if (l1 == null && l2 == null) {
               return null;
           } else {
               ListNode curr1 = l1;
               ListNode curr2 = l2;
               ListNode curr = null;
               int carry = 0;
               while (curr1 != null || curr2 != null) {
                   int value1 = curr1 == null ? 0 : curr1.val;
                   int value2 = curr2 == null ? 0 : curr2.val;
                   int newValue = (value1 + value2 + carry) % 10;
                   carry = (value1 + value2 + carry) / 10;
                   ListNode listNode = new ListNode(newValue);
                   if (head == null) {
                       head = listNode;
                       curr = head;
                   } else {
                       curr.next = listNode;
                       curr = curr.next;
                   }
                   curr1 = curr1 == null ? null : curr1.next;
                   curr2 = curr2 == null ? null : curr2.next;
               }
               if (carry == 1) {
                   ListNode listNode = new ListNode(carry);
                   curr.next = listNode;
               }
           }
           return head;
       }
   }
   ```
   开始的时候，想得很复杂，可能是受反转链表的影响，竟然将两链表先去反转，然后走进了死胡同。该题主要
   考虑进位，处理好了进位就几乎完成了解答。看了下网上的答案，自己最后对进位为1则加到最高位的处理
   显得多余，应该放到while循环中，增加一个判断条件即可。
   <br>
   3.[环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)
   ```
   public class Solution {
       public boolean hasCycle(ListNode head) {
           ListNode curr = li;
           Set set = new HashSet();
           while (curr != null) {
               if (set.contains(li)) {
                   return true;
               }
               set.add(curr);
               curr = curr.next;
           }
           return false;
       }
   }
   ```
   这个是看了网上的解答，而后才恍然大悟。利用了set的特性。但还有用快慢指针的，只要
   两者相等的时候不等于null，是不是就可以得出判断了呢？
   <br>
   4.[合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
   ```
   class Solution {
       public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
          ListNode se = new ListNode(-1);
          ListNode head = se;
          while (l1 != null || l2 != null) {
              int val = 0;
              if (l1 != null && l2 != null) {
                  if (l1.val < l2.val) {
                      val = l1.val;
                      l1 = l1.next;
                  } else {
                      val = l2.val;
                      l2 = l2.next;
                  }
              } else if (l1 == null && l2 != null) {
                  val = l2.val;
                  l2 = l2.next;
              } else {
                  val = l1.val;
                  l1 = l1.next;
              }
              ListNode newListNode = new ListNode(val);
              head.next = newListNode;
              head = head.next;
          }
          return se.next; 
       }
   }
   ```
   从这个算法开始，自己尝试开始用哨兵节点，慢慢体会它的妙出。
   <br>
   5.[删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
   ```
   class Solution {
       public ListNode removeNthFromEnd(ListNode head, int n) {
           LinkedList<ListNode> list = new LinkedList();
           ListNode curr = head;
           while (curr != null) {
               list.add(curr);
               curr = curr.next;
           }
   
           if (list.size() == n) {
               curr = head.next;
               head.next = null;
               head = curr;
               return head;
           } else if (n == 1) {
               curr = list.get(list.size() - n - 1);
               curr.next = null;
           } else {
               ListNode removeNode = list.get(list.size() - n);
               curr = list.get(list.size() - n - 1);
               curr.next = removeNode.next;
               removeNode.next = null;
           }
           return list.getFirst();
       }
   }
   ```
   我的解答是想着链表环的检测可以用Java自带的工具包，那这个无非就是要找出相应的索引，
   所以就用了List,从题的解答来看，自己完全走错了方向，虽然答案是正确的。汗颜。。。
   <br>
   看了官方答案，比较好的做法是用快慢指针，中间间隔为N，实在是巧妙。
   <br>
   6.[链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)
   ```
   class Solution {
       public ListNode middleNode(ListNode head) {
           ListNode se = new ListNode(-1);
           se.next = head;
           ListNode curr = head;
           int size = 0;
           while (curr != null) {
               ++size;
               curr = curr.next;
           }
           for(int index = 0, length = size/2; index <= length; ++index){
               se = se.next;
           }
           return se;
       }
   }
   ```
   <br>
   官方比较好的做法是用快慢指针，慢指针走一步，快指针走两步，思想甚是巧妙。
   <br>

# 阅读点评
   