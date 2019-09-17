```
use std::rc::Rc;
use std::cell::RefCell;

// Definition for a binary tree node.
#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
  pub val: i32,
  pub left: Option<Rc<RefCell<TreeNode>>>,
  pub right: Option<Rc<RefCell<TreeNode>>>,
}
// 
impl TreeNode {
  #[inline]
  pub fn new(val: i32) -> Self {
    TreeNode {
      val,
      left: None,
      right: None
    }
  }
}



struct Solution {
}

impl Solution {
    pub fn invert_tree(root: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
        match root {
            None => return None,
            Some(node) => {
                let left = (*(*node).borrow_mut()).left.take();
                let right = (*(*node).borrow_mut()).right.take();
                let left = Solution::invert_tree(left);
                let right = Solution::invert_tree(right);
                (*(*node).borrow_mut()).left = right;
                (*(*node).borrow_mut()).right = left;
                return Some(node);
            },
        }
    }

}



#[cfg(test)]
mod tests {
    use super::*;

    fn make_tree(list: &Vec<i32>, idx: usize) -> Option<Rc<RefCell<TreeNode>>> {
        if idx >= list.len() {
            return None;
        }
        let cur_node = Rc::new(RefCell::new(TreeNode::new(list[idx])));
        let l_idx = idx * 2 + 1;
        let r_idx = idx * 2 + 2;
        let lnode = make_tree(list, l_idx);
        let rnode = make_tree(list, r_idx);
        ((*cur_node).borrow_mut()).left = lnode;
        ((*cur_node).borrow_mut()).right = rnode;
        return Some(cur_node)
    }

    #[test]
    fn test_solution() {
        let tree1 = make_tree(&vec![4,2,7,1,3,6,9], 0);
        let tree2 = make_tree(&vec![4,7,2,9,6,3,1], 0);
        assert_eq!(Solution::invert_tree(tree1), tree2);
    }
}
```


## 性能

Runtime: 0 ms, faster than 100.00% of Rust online submissions for Invert Binary Tree.
Memory Usage: 2.4 MB, less than 100.00% of Rust online submissions for Invert Binary Tree.

## 思路

做一个递归的左右互换即可

## 复杂度
节点数量 N 的话，就是 O(N)

## 提升空间
非递归吧

## 困难点

没有什么困难，主要是rust语法的问题，编译了好几次

## 分类
Tree

## 类似题目

1) Minimum Height Trees
2) Maximum Binary Tree
3) Same Tree
