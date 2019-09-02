#AddTwoNumbers
##code
```
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
// 
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
impl Solution {
    pub fn add_two_numbers(l1: Option<Box<ListNode>>, l2: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        if l1.is_none() {
            return l2;
        }
        if l2.is_none() {
            return l1;
        }
        let mut n_l1 = &mut l1.unwrap();
        let mut n_l2 = &mut l2.unwrap();
        let mut add = 0;
        let mut red = 0;
        loop {
            let t = add + n_l1.val + n_l2.val;
            add = t / 10;
            red = t % 10;
            n_l1.val = red;
            if n_l1.next.is_none() || n_l2.next.is_none() {
                break;
            }
            
            n_l1.val = red;
            n_l1 = n_l1.next.as_mut().unwrap();
            n_l2 = n_l2.next.as_mut().unwrap();
        }
        if n_l1.next.is_none() {
            n_l1.next = n_l2.next.take();
            loop {
                if n_l2.next.is_none() {
                    break;
                }
                if add == 0 {
                    return l1;
                }
                n_l2 = &mut n_l2.next.unwrap();
                n_l2.val = (n_l2.val + 1) % 10;
                add = (n_l2.val + 1) / 10; 
            }
        }
        return l1;
    }
}
```
##思路

通过递归来实现链表元素加和，功能非常简单，忽略了c语言种修改链表元素值的方式来完成这道题。

### 复杂度
 O(n)
### 困难：
主要是不能够修改链表元素值，让我感觉多余的申请了空间，不知道还有没有别的更好的方案
### 可能的优化思路：
直接修改链表的值, 但是这个似乎对rust来说很困难
### 归类：
链表
### 类似题型：
#### 1) Reverse Nodes in k-Group
#### 2) Partition List
#### 3) Reverse Linked List
