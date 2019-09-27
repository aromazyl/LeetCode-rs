``` rust
use std::rc::Rc;
use std::cell::RefCell;

struct MyHashMap {
    mem: RefCell<[i32; 1000001]>,
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyHashMap {

    /** Initialize your data structure here. */
    fn new() -> Self {
        MyHashMap {
            mem: RefCell::new([-1; 1000001]),
        }
    }

    /** value will always be non-negative. */
    fn put(&self, key: i32, value: i32) {
        let key = key as usize;
        (*(self.mem.borrow_mut()))[key] = value;
    }

    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    fn get(&self, key: i32) -> i32 {
        let key = key as usize;
        self.mem.borrow()[key]
    }

    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    fn remove(&self, key: i32) {
        let key = key as usize;
        (*(self.mem.borrow_mut()))[key] = -1;
    }
}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * let obj = MyHashMap::new();
 * obj.put(key, value);
 * let ret_2: i32 = obj.get(key);
 * obj.remove(key);
 */

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_solution() {
        let obj = MyHashMap::new();
        obj.put(100, 101);
        let ret_2: i32 = obj.get(100);
        assert_eq!(ret_2, 101);
        obj.remove(100);
        let ret_2: i32 = obj.get(100);
        assert_eq!(ret_2, -1);
    }
}
```

## 性能

Runtime: 20 ms, faster than 97.62% of Rust online submissions for Reverse String.
Memory Usage: 5 MB, less than 100.00% of Rust online submissions for Reverse String.

## 思路

由于数据区间有限,直接使用array即可

## 复杂度

时间复杂度O(1), 空间复杂度O(1){1000001}

## 提升空间
实际上就是空间和时间的tradeoff, 可以选择一个优良的hash函数以及表大小来做优化

## 困难点

没有什么困难

## 分类
hash map

## 类似题目
1) Design Hash Set
2) Smallest Sufficient Team
3) Fair Candy Swap
