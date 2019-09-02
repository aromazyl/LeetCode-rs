#题目
AddTwoNumbers

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
pub fn add_two_numbers_n(l1: Option<Box<ListNode>>, l2: Option<Box<ListNode>>, add: i32) -> Option<Box<ListNode>> {
        if l1.is_none() {
            if l2.is_none() {
                if add != 0 {
                    return Some(Box::new(ListNode {
                        val: 1,
                        next: None,
                    }))
                }
                return None;
            }
            return add_two_numbers_n(l2, l1, add);
        }
        
        if l2.is_none() {
            if add == 0 {
                return l1;
            }
            let rl1 = l1.unwrap();
            let n_add = 1 + rl1.val;
            let r_add = n_add % 10;
            let add = n_add / 10;
            let kNode = add_two_numbers_n(rl1.next, None, add);
            return Some(Box::new(ListNode {
                val: r_add,
                next: kNode,
            }));
        }
        
        let rl1 = l1.unwrap();
        let rl2 = l2.unwrap();
        let n_add = add + rl1.val + rl2.val;
        let x_add = n_add / 10;
        let val = n_add % 10;
        let lNode = add_two_numbers_n(rl1.next, rl2.next, x_add);
        return Some(Box::new(ListNode{
            val,
            next: lNode,
        }))
    }
impl Solution {
    
    pub fn add_two_numbers(l1: Option<Box<ListNode>>, l2: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
       return add_two_numbers_n(l1, l2, 0);
    }
}
```

## 测试结果

Success
Details 
Runtime: 4 ms, faster than 82.69% of Rust online submissions for Add Two Numbers.
Memory Usage: 2.4 MB, less than 33.33% of Rust online submissions for Add Two Numbers.

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
